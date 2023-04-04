## Day One of building on Polkadot

### Mission; Build and start a single node block on Substrate.

### Step 1; Cloned the node template repo

```
git clone https://github.com/substrate-developer-hub/substrate-node-template
```

### Step2; Moved to the cloned repo

```
cd substrate-node-template
```

### Step3; Created a new branch

```
git switch -c my-learning-branch-2023-04-03
```

### Step4; Compile the node template by running the following command:

```
cargo build --release
```

It should start compiling this way;

```
hp@Cyndie:~/Desktop/30DaysOfPolkadot/day_one/substrate-node-template$ cargo build --release
    Updating crates.io index
  Downloaded atomic-waker v1.1.0
  Downloaded byte-tools v0.3.1
  Downloaded itoa v1.0.6
  Downloaded humantime v2.1.0
  Downloaded libsecp256k1-gen-ecmult v0.3.0
  Downloaded cipher v0.3.0
  Downloaded iana-time-zone v0.1.54
  Downloaded httparse v1.8.0
  Downloaded bytes v1.4.0
  Downloaded libp2p-wasm-ext v0.38.0
  Downloaded keccak v0.1.3
  Downloaded adler v1.0.2
  Downloaded libp2p-yamux v0.42.0
  Downloaded hex v0.4.3
  Downloaded asn1-rs-derive v0.1.0
  Downloaded cargo-platform v0.1.2
  Downloaded http-body v0.4.5
  Downloaded block-padding v0.1.5
.....
```

### Errors encountered in this stage;

### 1. `Wasm` tool not installed

```
error: failed to run custom build command for `node-template-runtime v4.0.0-dev (/home/hp/Desktop/30DaysOfPolkadot/day_one/substrate-node-template/runtime)`

Caused by:
  process didn't exit successfully: `/home/hp/Desktop/30DaysOfPolkadot/day_one/substrate-node-template/target/release/build/node-template-runtime-34984fc9b9a18fb2/build-script-build` (exit status: 1)
  --- stderr
  Rust WASM toolchain not installed, please install it!

  Further error information:
  ------------------------------------------------------------
     Compiling wasm-test v1.0.0 (/tmp/.tmp7ulqkg)
  error[E0463]: can't find crate for `std`
    |
    = note: the `wasm32-unknown-unknown` target may not be installed
    = help: consider downloading the target with `rustup target add wasm32-unknown-unknown`
    = help: consider building the standard library from source with `cargo build -Zbuild-std`

  error: requires `sized` lang_item

  For more information about this error, try `rustc --explain E0463`.
  error: could not compile `wasm-test` (lib) due to 2 previous errors
  warning: build failed, waiting for other jobs to finish...
  error: cannot find macro `println` in this scope


```

Resolved this by installing `wasm` tool;

```
hp@Cyndie:~/Desktop/30DaysOfPolkadot/day_one/substrate-node-template$ rustup target add wasm32-unknown-unknown
info: downloading component 'rust-std' for 'wasm32-unknown-unknown'
info: installing component 'rust-std' for 'wasm32-unknown-unknown'
 18.1 MiB /  18.1 MiB (100 %)  11.5 MiB/s in  1s ETA:  0s

```

### N.B This is what I started with in my Rust Toolchain;

```
hp@Cyndie:~/Desktop/30DaysOfPolkadot/day_one/substrate-node-template$ rustup show
Default host: x86_64-unknown-linux-gnu
rustup home:  /home/hp/.rustup

installed toolchains
--------------------

stable-x86_64-unknown-linux-gnu
nightly-x86_64-unknown-linux-gnu (default)

active toolchain
----------------

nightly-x86_64-unknown-linux-gnu (default)
rustc 1.70.0-nightly (cf7ada217 2023-04-03)

```

### Compiling the node template occured successfully then;

```
    Finished release [optimized] target(s) in 44m 14s

```

### Step5; Started the local node compiled;

```
hp@Cyndie:~/Desktop/30DaysOfPolkadot/day_one/substrate-node-template$ ./target/release/node-template --dev
2023-04-04 21:18:47 Substrate Node    
2023-04-04 21:18:47 ✌️  version 4.0.0-dev-700c3a186e5    
2023-04-04 21:18:47 ❤️  by Substrate DevHub <https://github.com/substrate-developer-hub>, 2017-2023    
2023-04-04 21:18:47 📋 Chain specification: Development    
2023-04-04 21:18:47 🏷  Node name: abrasive-quiver-2825    
2023-04-04 21:18:47 👤 Role: AUTHORITY    
2023-04-04 21:18:47 💾 Database: RocksDb at /tmp/substrateAMC6p6/chains/dev/db/full    
2023-04-04 21:18:47 ⛓  Native runtime: node-template-100 (node-template-1.tx1.au1)    
Error: Service(Client(VersionInvalid("cannot deserialize module: UnknownOpcode(192)")))
2023-04-04 21:18:48 Cannot create a runtime error=Other("cannot deserialize module: UnknownOpcode(192)")

```

### Error encountered; 
```
Error: Service(Client(VersionInvalid("cannot deserialize module: UnknownOpcode(192)")))
2023-04-04 21:18:48 Cannot create a runtime error=Other("cannot deserialize module: UnknownOpcode(192)")

```
The error indicates that the client is unable to parse or understand a specific opcode used in the code. 

This can happen when using a version of the client that is not compatible with the code being executed.



### N.B. Errors encountered installing `yarn`

### Realized I didn't have `yarn` installed;

```
yarn --version

Command 'yarn' not found, but can be installed with:

sudo apt install cmdtest


```
### Installed `yarn` using `sudo apt install cmdtest` command;

```
hp@Cyndie:~/Desktop/30DaysOfPolkadot/day_one/substrate-node-template$ sudo apt install cmdtest
[sudo] password for hp: 
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following additional packages will be installed:
  python3-cliapp python3-markdown python3-packaging python3-pyparsing python3-ttystatus
Suggested packages:
  python-markdown-doc python-pyparsing-doc
The following NEW packages will be installed:
cmdtest python3-cliapp python3-markdown python3-packaging python3-pyparsing python3-ttystatus
.....
```

### Checked the `yarn` version;

```
yarn --version
0.32+git
```

### For this tutorial atleast `yarn v3` was needed; tried upgrading it;

```
 yarn self-update
00h00m00s 0/0: : ERROR: [Errno 2] No such file or directory: 'self-update'

```

### Checked online; `yarn self-update` was not being used anymore; Tried `npm install -g yarn@3`

```
hp@Cyndie:~/substrate-front-end-template$ npm install -g yarn@3
npm ERR! code ETARGET
npm ERR! notarget No matching version found for yarn@3.
npm ERR! notarget In most cases you or one of your dependencies are requesting
npm ERR! notarget a package version that doesn't exist.

npm ERR! A complete log of this run can be found in:
npm ERR!     /home/hp/.npm/_logs/2023-04-04T18_49_52_456Z-debug-0.log

```

### Used `corepack` binary tool found in `node.js`; Enabled it first;

```
corepack enable
```

### Updated the global yarn version using corepack;

```
corepack prepare yarn@stable --activate
```

### Checked the yarn version again;

```
yarn --version
3.1.1

```



