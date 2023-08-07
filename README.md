## Prerequisites 

To get started, install: 

- Rust 
`$ curl --proto '=https' --tlsv1.2 https://sh.rustup.rs -sSf | sh`


- nightly toolchain 

`rustup toolchain install nightly`
`rustup target add wasm32-unknown-unknown --toolchain nightly`

- only on Mac 
`xcode-select --install`

Clone, build, and run [Madara repository](https://github.com/keep-starknet-strange/madara)

`git clone https://github.com/keep-starknet-strange/madara.git`
`cargo +nightly build --release`
`cargo +nightly run --release -- --dev`

Head to the [explorer](https://polkadot.js.org/apps/#/explorer) and verify that your local node is producing blocks!


## Scarb package manager

Optionally, take the pre-built contracts from the scripts. 

To build your own Cairo contracts, you will need the scarb package manager:

`curl --proto '=https' --tlsv1.2 -sSf https://docs.swmansion.com/scarb/install.sh | sh -s -- -v 0.5.0`

There is a later version of scarb available, but for the current Cairo VM verison in Madara we require 0.5.0. 

Run `mkdir workshop` && `cd workshop`.
Inside the project folder, run `scarb init`.

In `Scarb.toml`, add the following:

```
[package]
name = "workshop"
version = "0.1.0"

# See more keys and their definitions at https://docs.swmansion.com/scarb/docs/reference/manifest

[dependencies]
starknet = "2.0.0"

[[target.starknet-contract]]
sierra = true
casm = true
```

The above is necessary to have both `sierra` and `casm` generated. 

In `src/lib.rs`, add the following code from the [erc20 contract](https://github.com/keep-starknet-strange/madara/blob/main/cairo-contracts/src/cairo_1/erc20/erc20.cairo).

To compile a Cairo contract, run `scarb build`.


## Deploying contracts 

Clone [script repo](https://github.com/lana-shanghai/madara_contract_scripts)

Run `npm install` and `node index.js`. This should show the last block finalized on Madara.

Test deployment of pre-built contracts: 

`node declare_hello_starknet.js`
`node deploy_hello_starknet.js`

Before invoking a contract, make sure to add the contract address to the invoke script. It can be fetched from `deployResponse.contract_address`, or from the terminal.

`node invoke_hello_starknet.js`

