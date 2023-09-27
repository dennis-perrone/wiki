# How to encrypt PDFs

Created: 2023-09-26

## Notes

- To encrypt:
  - Install the `qpdf` package.
  - Run `qpdf --encrypt <user_passwd> <owner_passwd> 256 -- input.pdf output.pdf`
- To decrypt:
  - `qpdf --password=<PASSWORD> --decrypt encrypted.pdf decrypted.pdf`

## References

1. [FOSTips: How to encrypt/decrypt](https://fostips.com/encrypt-decrypt-pdf-ubuntu-fedora-linux/)
