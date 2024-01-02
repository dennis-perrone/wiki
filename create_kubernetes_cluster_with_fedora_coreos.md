# Create Kubernetes Cluster with Fedora CoreOS

- Created:  2024-01-02 04:30:04 EST
- Modified: 2024-01-02 04:30:04 EST

## Notes

### Prerequisites

- Download CoreOS qcow2 image from the [download site](https://fedoraproject.org/en/coreos/download?stream=stable).
- Decompress the `.xz` by using `unxz`.
- Ensure there is an SSH key present on your machine.
- A KVM hypervisor with bridge interface (`br0`) configured.

### Steps

1. Create an ignition script using Butane and paste the following into `fcos.bu`. Update the public SSH key. **NOTE:** As of 2023-12-15, set `repo_gpgcheck=0`

```yaml
variant: fcos
version: 1.4.0
storage:
	files:
 		# CRI-O DNF module
    - path: /etc/dnf/modules.d/cri-o.module
     	mode: 0644
     	overwrite: true
     	contents:
       	inline: |
         	[cri-o]
         	name=cri-o
         	stream=1.17
         	profiles=
         	state=enabled
     # YUM repository for kubeadm, kubelet and kubectl
     - path: /etc/yum.repos.d/kubernetes.repo
       mode: 0644
       overwrite: true
       contents:
         inline: |
           [kubernetes]
           name=Kubernetes
           baseurl=https://packages.cloud.google.com/yum/repos/kubernetes-el7-x86_64
           enabled=1
           gpgcheck=1
           repo_gpgcheck=1
           gpgkey=https://packages.cloud.google.com/yum/doc/yum-key.gpg
             https://packages.cloud.google.com/yum/doc/rpm-package-key.gpg
     # configuring automatic loading of br_netfilter on startup
     - path: /etc/modules-load.d/br_netfilter.conf
       mode: 0644
       overwrite: true
       contents:
         inline: br_netfilter
     # setting kernel parameters required by kubelet
     - path: /etc/sysctl.d/kubernetes.conf
       mode: 0644
       overwrite: true
       contents:
         inline: |
           net.bridge.bridge-nf-call-iptables=1
           net.ipv4.ip_forward=1
passwd:
  users:
    - name: core
      ssh_authorized_keys:
        - <PASTE YOUR SSH PUBLIC KEY HERE>
```

2. Paste the following into `start_fcos.sh`. **NOTE:** Update the `IGN_CONFIG` and `IMAGE` paths relevant to local environment.

```bash
#!/bin/sh

IGN_CONFIG=$HOME/k8s/fcos.ign
IMAGE=$HOME/k8s/fedora-coreos-39.20231119.3.0-qemu.x86_64.qcow2
VM_NAME=k8s-node$1
VCPUS=2
RAM_MB=4096
DISK_GB=20
STREAM=stable

chcon --verbose --type svirt_home_t ${IGN_CONFIG}
virt-install --connect="qemu:///system" --name="${VM_NAME}" \
    --vcpus="${VCPUS}" --memory="${RAM_MB}" \
    --os-variant="fedora-coreos-$STREAM" --import \
    --disk="size=${DISK_GB},backing_store=${IMAGE}" \
    --network bridge="br0" \
    --qemu-commandline="-fw_cfg name=opt/com.coreos/config,file=${IGN_CONFIG}"
```

3. Open 3 separate terminals and run `./start_fcos.sh 01`, `./start_fcos.sh 02`, and `./start_fcos.sh 03` on each separate terminal.
4. Once VM's are initialized, add the IP addresses into `/etc/hosts`.
5. Log into each node and run the following commands and set the relevant hostname for each node (either `node01`, `node02`, or `node03`):
	
```bash
sudo -i
echo "node01" > /etc/hostname
```

6. On `node01` (the control plane), run the following commands:

```bash
sudo rpm-ostree install kubelet kubeadm kubectl cri-o
sudo systemctl reboot
```

7. On `node02` and `node03`, run the following commands:
	
```bash
sudo rpm-ostree install kubelet kubeadm cri-o
sudo systemctl reboot
```

8. Log into each host after reboot and run the following command:

```bash
sudo systemctl enable --now crio kubelet
```

9. Log into `node01` and create `clusterconfig.yml`:
	
```yaml
apiVersion: kubeadm.k8s.io/v1beta3
kind: ClusterConfiguration
kubernetesVersion: v1.28.2
controllerManager:
  extraArgs:
    flex-volume-plugin-dir: "/etc/kubernetes/kubelet-plugins/volume/exec"
networking: # pod subnet definition
 	podSubnet: 10.244.0.0/16
---
apiVersion: kubeadm.k8s.io/v1beta3
kind: InitConfiguration
```

10. Run `kubeadm init --config clusterconfig.yml`
11. Configure `kubectl` on the control plane:

```bash
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

12. Set up pod networking:

```bash
kubectl apply -f https://raw.githubusercontent.com/cloudnativelabs/kube-router/master/daemonset/kubeadm-kuberouter.yaml
```

13. Generate the join token:

```bash
kubeadm token create –-print-join-command`
```

14. Log into `node02` and `node03` and execute the "join" command generated in the previous step.
15. Verify that all nodes are part of the cluster by running `kubectl get nodes` on `node01`

## References

1. [Creating a Kubernetes Cluster with Fedora CoreOS 36](https://dev.to/carminezacc/creating-a-kubernetes-cluster-with-fedora-coreos-36-j17)
