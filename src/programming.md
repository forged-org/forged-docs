# Programming Firmware

Firmware is programmed onto devices by adding a "Flash Chip" step to your project's playbook. The
step selects a chip from your project, and the provisioner programs the newest binary uploaded for
that chip.

## Uploading Binaries

Binaries are uploaded to a chip from the chip's page in the forged.dev UI. A binary may consist of
one or more parts, each of which is a separate file.

The format of each part is determined by its file extension:

| Extension | Format |
| :-------: | :----- |
| `.elf` | ELF executable |
| `.hex` | Intel HEX |
| `.bin` | Raw binary |

Files with any other extension are treated as ELF files.

The original filename of each part is stored alongside the binary. The provisioner uses this name
when it saves the part to disk, which is useful for programming tools that rely on the file name or
extension.

## Programming with probe-rs

If the selected chip is supported by [`probe-rs`](https://probe.rs), the provisioner programs the
device directly using the connected debug probe. No additional configuration is required.

When programming with probe-rs, the provisioner also:
* Reads `Device Memory` data blocks from the device before programming
* Writes data blocks configured to persist to the device after programming
* Resets the device and collects data blocks over RTT (see
  [Uploading Block Data during Provisioning](./data-blocks.md#uploading-block-data-during-provisioning))

## Custom Programming Commands

A programming step may optionally specify a custom programming command. When a command is provided,
the provisioner runs it to program the device instead of using probe-rs. This allows you to use
vendor-specific programming tools, or to program chips that are not supported by probe-rs.

A custom programming command is required for chips that are not supported by probe-rs, and is
optional for all other chips.

### The `{BINARY}` Placeholder

Before running the command, the provisioner downloads each binary part and replaces the `{BINARY}`
placeholder in the command with the path to the downloaded file. For example, the command:

```
nrfjprog --program "{BINARY}" --chiperase --verify --reset
```

will be run as:

```
nrfjprog --program "/home/operator/.local/share/dev.forged.provisioner/5f0c.../firmware.hex" --chiperase --verify --reset
```

If the command does not contain `{BINARY}`, the path to the binary is appended to the end of the
command instead.

If a binary consists of multiple parts, the command is run once for each part, in order, with
`{BINARY}` referring to the current part.

If the command exits with a non-zero exit code, programming is considered to have failed and the
run fails. Any remaining binary parts are not programmed.

> **Tip:** The path to the binary may contain spaces, especially on Windows. Wrap the placeholder
> in quotes, as in `"{BINARY}"`, to ensure the path is passed to your tool as a single argument. A
> path that is appended automatically is not quoted.

### Command Environment

Custom programming commands are run through the system shell (`sh -c` on Linux and macOS,
`cmd /C` on Windows), so shell features such as pipes and environment variable expansion are
available.

The output of the command is shown in the provisioner UI and uploaded as the `command.log` log of
the device. Lines printed by the command in the form `forged>{block-name}:{block-value}` are
uploaded as data blocks, in the same manner as
[RTT block uploads](./data-blocks.md#uploading-block-data-during-provisioning).

### Limitations

When a custom programming command is used, the provisioner does not connect to the device with
probe-rs. As a result:
* `Device Memory` data blocks are not read from the device
* Data blocks are not written to the device after programming
* Data blocks are not collected over RTT

If your project relies on any of these features for a chip that is supported by probe-rs, leave the
programming command empty.
