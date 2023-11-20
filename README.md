# staking-cli

## Introduction

`deposit-cli` is a tool for creating [EIP-2335 format](https://eips.ethereum.org/EIPS/eip-2335) BLS12-381 keystores and a corresponding `deposit_data*.json` file for [Ethereum Staking Launchpad](https://github.com/engram-network/staking-launchpad).

- **Warning: Please generate your keystores on your own safe, completely offline device.**
- **Warning: Please backup your mnemonic, keystores, and password securely.**

Please read [Launchpad Validator FAQs](https://launchpad.engram.tech/faq#keys) before generating the keys.

## Tutorial for users

### Build requirements

- [Python **3.8+**](https://www.python.org/about/gettingstarted/)
- [pip3](https://pip.pypa.io/en/stable/installing/)

### For Linux or MacOS users

#### File Permissions

On Unix-based systems, keystores and the `deposit_data*.json` have `440`/`-r--r-----` file permissions (user & group read only). This improves security by limiting which users and processes that have access to these files. If you are getting `permission denied` errors when handling your keystores, consider changing which user/group owns the file (with `chown`) or, if need be, change the file permissions with `chmod`.


Run the following command to enter the interactive CLI and generate keys from a new mnemonic:

```sh
./deposit new-mnemonic
```

or run the following command to enter the interactive CLI and generate keys from an existing:

```sh
./deposit existing-mnemonic
```

##### Step 1. Installation

Install the dependencies:

```sh
pip3 install -r requirements.txt
python3 setup.py install
```

Or use the helper script:

```sh
./deposit.sh install
```

##### Step 2. Create keys and `deposit_data-*.json`

Run one of the following command to enter the interactive CLI:

```sh
./deposit.sh new-mnemonic
```

or

```sh
./deposit.sh existing-mnemonic
```

You can also run the tool with optional arguments:

```sh
./deposit.sh new-mnemonic --num_validators=<NUM_VALIDATORS> --mnemonic_language=english --chain=<CHAIN_NAME> --folder=<YOUR_FOLDER_PATH>
```

```sh
./deposit.sh existing-mnemonic --num_validators=<NUM_VALIDATORS> --validator_start_index=<START_INDEX> --chain=<CHAIN_NAME> --folder=<YOUR_FOLDER_PATH>
```

##### Build the docker image

Run the following command to locally build the docker image:

```sh
make build_docker
```

##### Step 2. Create keys and `deposit_data-*.json`

Run the following command to enter the interactive CLI:

```sh
docker run -it --rm -v $(pwd)/validator_keys:/app/validator_keys engramnet/staking-deposit-cli
```

You can also run the tool with optional arguments:

```sh
docker run -it --rm -v $(pwd)/validator_keys:/app/validator_keys engramnet/staking-deposit-cli new-mnemonic --num_validators=<NUM_VALIDATORS> --mnemonic_language=english --folder=<YOUR_FOLDER_PATH>
```

Example for 1 validator on the [Tokio testnet](https://launchpad.engram.tech/) using english:

```sh
docker run -it --rm -v $(pwd)/validator_keys:/app/validator_keys engramnet/staking-deposit-cli new-mnemonic --num_validators=1 --mnemonic_language=english --chain=testnet
```