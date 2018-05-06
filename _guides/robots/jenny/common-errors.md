This document lists various common errors on Jenny and working solutions to those.

# CAN Devices Not Recognised

This error might appear after upgrading the kernel on Jenny's PCs.

Reinstalling the CAN device driver is a working fix of the error.
To ensure that there are no compatibility issues with the gripper, rather than installing a new version of the driver, the CAN driver in [`cob_extern`](https://github.com/mas-group/cob_extern) should be installed (current stable version `7.15.2`).
