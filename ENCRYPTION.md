# Monetary Payment Data Encryption (E2EE)

### Encryption Protocols

We utilize industry standard encryption ([3DES](https://en.wikipedia.org/wiki/Triple_DES) + [DUKPT](https://en.wikipedia.org/wiki/Derived_unique_key_per_transaction)) to secure account information transmitted to and received by our servers.

### Hardware

We have partnered with hardware manufacturers and distrubutors to provide secure encryption devices with Monetary's encryption keys.

* **ID TECH**<br />ID TECH devices should be configured to use `Enhanced Encrypted Data Structure Format`. This allows for integrators to extract the KSN (key serial number) and encrypted track 2 block from the device payload, as track 1 and track 2 are encrypted in different blocks.
