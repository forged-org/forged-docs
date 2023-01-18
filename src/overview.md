# Overview

Forged is a manufacturing and device provisioning tool. It is designed to be a swiss army knife of
the embedded manufacturing process.

Some notable features:
* Forged.dev tracks and stores data associated with every device manufactured, including:
    * User-provided parameters (such as serial numbers)
    * Measured values (such as voltage measurements performed during testing)
    * Queried values (such as chip UUIDs and MAC addresses programmed by chip manufacturers)
    * Generated values (such as device-specific calibration coefficients generated from other
            parameters)
    * Logs associated with the provisioning process

* Forged.dev provides cloud-based storage and retrieval of released firmware images, which allows:
    * Automated incorporation of firmware releases directly into manufacturing processes
    * A single source for firmware delivery to any number of distributed machines
    * Tracking of firmware statistics over time, such as flash utilization rates
    * Tracking of all released firmware variants
    * Associating specific firmware releases with specific devices

* Forged.dev provides an adaptive GUI for the device provisioning process
    * GUI adapters to the project parameters to automatically follow a provisioning process

* Forged.dev supports formal requirements and manufacturing testing
    * Data collected during the provisioning process is automatically checked against specified
    requirements to determine passing and failing units automatically.
