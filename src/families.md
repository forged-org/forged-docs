# Custom Chips

Forged supports custom chip specifications if you have a chip that is not supported out-of-the-box.

## Description Generation
[`target-gen`](https://crates.io/crates/target-gen) can be used to automatically generate
specification files for ingestion into forged.dev (and `probe-rs`) from ARM CMSIS packs quickly.

## Implementaton Details
Custom chip descriptions are added to the [`probe-rs`](https://docs.rs/probe-rs/latest/probe_rs)
implementation leveraged by the forged.dev backend and provisioner utilities. The description tells
the flashing utility about what memory sections are present and what algorithms should be used to
flash the device.

See the [`probe-rs` documentation](https://docs.rs/probe-rs/latest/probe_rs) for more information.

## Limitations

* Any custom chips uploaded are currently accessible to all users, not just your account.
