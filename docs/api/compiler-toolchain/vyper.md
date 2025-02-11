# Vyper

The Vyper compiler we provide as part of our toolchain is called [zkvyper](https://github.com/matter-labs/zkvyper-bin). It
operates on Vyper’s LLL IR, and metadata received from the underlying [vyper](https://docs.vyperlang.org/en/latest/index.html) compiler,
which must be available in `$PATH`, or its path must be explicitly passed via the CLI (command-line interface).

## Usage

Make sure your machine satisfies the [system requirements](https://github.com/matter-labs/era-compiler-vyper/tree/main#system-requirements).

Using our compiler via the Hardhat plugin usually suffices. However, knowledge of its interface and I/O (input/output)
methods are crucial for integration, debugging, or contribution purposes.

#### Combined JSON

The `zkvyper` standard JSON I/O workflow closely follows that of the official `vyper` compiler. However, `zkvyper` does not
support some configuration settings which are only relevant to the EVM architecture.

Combined JSON is only an output format; there is no combined JSON input format. Instead, CLI arguments are
used for configuration.

Additional zkEVM data is inserted into the output combined JSON by `zksolc`:

- `zk_version`: the `zksolc` version.
- `contract/factory_deps`: bytecode hashes of contracts created in the current contract with `CREATE`.
  Since Vyper does not support `CREATE` directly, only the forwarder can be present in this mapping.
   [More detail here](../../dev/building-on-zksync/contracts/contract-deployment.md#note-on-factorydeps).

Regardless of the requested output, only the `combined_json`, `abi`, `method_identifiers`, `bytecode`, `bytecode_runtime`
flags are supported, while the rest are ignored.

Other output formats are available via the `-f` option. Check out `vyper --help` for more details.

## Limitations

Currently only Vyper v0.3.3 is supported.
