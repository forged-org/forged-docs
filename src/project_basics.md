# Forged Projects

Projects are the heart of the forged.dev workflow. All activity happens within a forged.dev project.

Once your project is created, you can:
* Upload firmware releases
* Provision and track newly manufactured devices
* Set up provisioning hardware for the manufacturing process
* Specify data associated with devices

Forged.dev projects have a few fundamental building blocks that we'll go over here to explain how
forged.dev works. A brief overview of the fundamentals is provided below. Please refer to the
respective documentation page for further information on these concepts.

### Devices

When you create a new project, the `Devices` tab records all of the devices that are manufactured
with this project. Each device tracks:
* Measurements associated with the device
* Device-specific data, such as serial numbers
* Logs from the manufacturing and provisioning process
* Attachments from the provisioning process
* Provisioning status (pass/fail results)
* Other device-specific information

#### Device Runs

A single device may be processed through the provisioning process multiple times. This can occur for
a variety of reasons, such as equipment operating incorrectly during the provisioning process, or as
a result of identified and corrected issues in the hardware being tested. Each of these passes
through the provisioning process is tracked as a separate "run" for a single device.

There is no limit to the number of runs that can be associated with a device.

### Requirements

Requirements are a method to verify that your device is operating to required specifications before
determining if it is passing or failing the manufacturing process.

Forged uses requirements to automatically check measured data against pre-specified requirements at
the end of the provisioning process. If all the required data is present and within specification,
the device is considered to have passed provisioning. If data is absent, a step in the provisioning
process fails, or if data is specified outside of required tolerances, the device run is marked as
failing.

### Data Blocks

Data blocks represent what data is associated with a device. Blocks specify the format and content
of the data, as well as where the data originates from. The "Data Block" outlines the schematic for
what data will be associated with your manufactured devices before the process completes.

Requirements are always tested against a specific data block.

### Provisioners

Provisioners are the computer that actually performs the provisioning process. These computers have
a programmer connected to them (often via a USB cable) that connects to the hardware that is being
provisioned.

Forged provides two workflows for the provisioner:
1. The provisioner can use the Provisioner UI to automate the provisioning process in a
   user-friendly manner
2. API clients are provided for many languages to allow you to manually drive and customize the
   entire provisioning process.
