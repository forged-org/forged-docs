# Getting Started

You can get started with forged.dev quickly and easily be following a few basic steps:

### 1. Set up a project

The first step in getting started with forged.dev requires you to set up a project. Each project
describes a single product that is being manufactured. Setting up a project is as simple as giving
it a name and selecting what chip your project is targetting.

#### Note

Note that forged.dev (currently) primarily supports most ARM Cortex-M and RISC-V processors.

If your project is using another processor, forged.dev can still be used, but some features may have
reduced functionality. For example, if you use a processor that is not listed, the below limitations
apply:
* The provisioner UI cannot be used if you need to read or write device memory. In this case, you
  will have to use the forged.dev API clients directly and implement your own methods of reading and
  writing device memory.
    * This applies to having a binary uploaded for the project, or for data blocks that need to be
      written to device memory.


### 2. (Optional) Specify device data

Once you have created your project, you will need to specify the data that will be associated with
each device. Create any number of data blocks that your device has specified.

Some examples of data blocks include:
* Device serial numbers
* Manufacturing test measurements
    * Supply voltage measurements
    * Current usage measurements
* Device wireless identifiers (e.g. Bluetooth UUID, Ethernet MAC address)

### 3. (Optional) Specify device requirements

Once you have set up your required data blocks, create any requirements that a device must meet
before passing the provisioning process. These requirements will be checked at the end of the
provisioning process to verify that the device is operating within required specifications.

Some examples of requirements include:
* Limitations on the range of supply voltage measurements
* Maximum operating current limits

### 4. (Optional) Upload a binary

If your project has firmware that needs to be programmed onto the device, you can upload the
firmware build directly to forged.dev to be programmed onto your device during the provisioning
process. Upload your compiled firmware image to forged.dev with an associated version to add it to
your project provisioning process.


### 5. Configure a provisioner

Now that the rest of the project is set up, you'll need to set up a provisioner responsible for
executing the device provisioning process. The provisioner is a computer that communicates over the
internet with forged.dev, and is responsible for:
* Programming firmware onto your device
* Conducting device measurements and executing manufacturing tests
* Collecting device-specific information, such as serial numbers

Forged.dev provides an out-of-the-box provisioner user interface for all major operating systems
that enables you to quickly get a provisioner set up. You can install the provisioner utility from
the "Releases" tab of the forged.dev website.

If your project has more complex requirements that the provided provisioner utility cannot support,
you can create your own provisioner tools using the forged.dev API clients. Forged currently
maintains API clients for the following languages:
* `Rust`
* `Python`

If you need an API client for a language not yet supported, please get in contact with forged.dev.
It's also possible to develop custom clients to talk to the forged.dev website to drive the
manufacturing provisioning process. Forged.dev uses a GraphQL API, so custom clients can be made for
almost any language.

### 5. Provision a device

Once your provisioner is set up, you can provision your very first device. Connect your device to a
supported programming probe and start the provisioning process. Your device will automatically
appear in the forged.dev website under the "Devices" tab of your project.
