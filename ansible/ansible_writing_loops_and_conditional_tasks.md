# Writing Loops and Conditional Tasks in Ansible

## Notes

- A use case for a loop is if a module is being used multiple times within the same *play*.
- Loops help performance and also help with readability.
- Run a loop by:
  - Defining the list of variables within a dictionary
  - Within the task, `loop: "{{ var_name }}"`
  - For the item that needs to be looped over, `name: "{{ item }}"`
  - Example: Create a user:  

    ```yaml
    vars:
      my_users:
        - user01
        - user02
        - user03
    tasks:
      - name: Create users
        loop: "{{ my_users }}"
        anisble.builtin.user:
          name: "{{ item }}"
          state: "{{ my_state | default('present') }}"
          password: <value>
          update_password: on_create
      ```

- BEST PRACTICE: Put the module as the last part of the task. 
- Conditional values

| Operation                                                                  | Condition                                          |
| -----                                                                      | -----                                              |
| Equal (value is a string)                                                  | ansible_facts['machine'] == "x86_64                |
| Equal (value is numeric)                                                   | max_memory == 512                                  |
| Less than                                                                  | min_memory < 256                                   |
| Greater than                                                               | min_memory > 256                                   |
| Less than or equal to                                                      | min_memory <= 256                                  |
| Greater than or equal to                                                   | min_memory >= 256                                  |
| Not equal to                                                               | min_memory != 256                                  |
| Variable exists                                                            | min_memory is defined                              |
| Variable does not exist                                                    | min_memory is not defined                          |
| Boolean variable is true. The values of 1, True, or yes                    | memory_available                                   |
| Boolean variable is false. Tha values of 0, False, or no                   | not memory_available                               |
| First variable's value is present as a value is the second variable's list | ansible_facts['distribution'] in supported_distros |
