# Contributing

Thank you for wanting to contribute! This project reviews PRs that have an associated issue with
them. If you have not opened an issue for your PR, please create one first.

Issues, feedback, and sharing that you're using Moccasin on social media is always welcome!

# Table of Contents

- [Contributing](#contributing)
- [Table of Contents](#table-of-contents)
- [Setup](#setup)
  - [Manual Setup Requirements](#manual-setup-requirements)
    - [ZKsync requirements](#zksync-requirements)
  - [Dev Container Setup Requirements](#dev-container-setup-requirements)
  - [Installing for local development (Manual)](#installing-for-local-development-manual)
  - [Installing for local development (Dev Container)](#installing-for-local-development-dev-container)
  - [Running Tests](#running-tests)
    - [Local Tests](#local-tests)
    - [Integration Tests](#integration-tests)
    - [ZKsync Tests](#zksync-tests)
    - [Live Tests](#live-tests)
- [Code Style Guide](#code-style-guide)
  - [Where do you get the `typecheck` and `format` command?](#where-do-you-get-the-typecheck-and-format-command)
- [Editing documentation](#editing-documentation)
- [Thank you!](#thank-you)

# Setup

## Manual Setup Requirements

You must have the following installed to proceed with contributing to this project. 

- [git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
  - You'll know you did it right if you can run `git --version` and you see a response like `git version x.x.x`
- [python](https://www.python.org/downloads/)
  - You'll know you did it right if you can run `python --version` and you see a response like `Python x.x.x`
- [uv](https://docs.astral.sh/uv/getting-started/installation/)
  - You'll know you did it right if you can run `uv --version` and you see a response like `uv 0.4.7 (a178051e8 2024-09-07)`
- [anvil](https://book.getfoundry.sh/reference/anvil/)
  - You'll know you did it right if you can run `anvil --version` and you see a response like `anvil 0.2.0 (b1f4684 2024-05-24T00:20:06.635557000Z)`
- Linux and/or macOS
  - This project is not tested on Windows, so it is recommended to use a Linux or macOS machine, or use a tool like [WSL](https://learn.microsoft.com/en-us/windows/wsl/install) for Windows users.
- [just](https://github.com/casey/just)
  - You'll know you did it right if you can run `just --version` and you see a response like `just 1.35.0`

### ZKsync requirements
If you wish to run the ZKsync tests, you'll need these as well (run with `just test-z`)

- [anvil-zksync](https://github.com/matter-labs/anvil-zksync)
  - You'll know you did it right if you can run `anvil-zksync --version` and you see a response like `anvil-zksync 0.2.1`
- [era-compiler-vyper](https://github.com/matter-labs/era-compiler-vyper)
  - You'll know you did it right if you can run `zkvyper --version` and you see a response like `Vyper compiler for ZKsync v1.5.4 (LLVM build f9f732c8ebdb88fb8cd4528482a00e4f65bcb8b7)`

## Dev Container Setup Requirements

- [Docker](https://www.docker.com/)
  - You'll know you did it right if you can run `docker --version` and you see a response like `Docker version x.x.x, build xxxxxxx`
- [VSCode](https://code.visualstudio.com/)


## Installing for local development (Manual)

Follow the steps to clone the repo for you to make changes to this project.

1. Clone the repo

```bash
git clone https://github.com/cyfrin/moccasin
cd moccasin
```

2. Sync dependencies

*This repo uses uv to manage python dependencies and version. So you don't have to deal with virtual environments (much)*

```bash
uv sync --all-extras
```

3. Create a new branch

```bash
git checkout -b <branch_name>
```

And start making your changes! Once you're done, you can commit your changes and push them to your forked repo.

```bash
git add .
git commit -m 'your commit message'
git push <your_forked_github>
```

4. Virtual Environment

You can then (optionally) work with the virtual environment created by `uv`.

```bash
source .venv/bin/activate
```

And to remove the virtual environment, just run:
```bash
deactivate
```

However, if you run tests and scripts using the `uv` or `just` commands as we will describe below, you won't have to worry about that. 

*Note: When you delete your terminal/shell, you will need to reactivate this virtual environment again each time. To exit this python virtual environment, type `deactivate`*

## Installing for local development (Dev Container)

1. Clone the repo

```bash
git clone https://github.com/cyfrin/moccasin
cd moccasin
```

2. Start the dev container

Open the repo in VSCode and you should see a prompt to open the repo in a dev container. Click on that and it will start the dev container for you.

This will:
1. Install the required dependencies
2. Set up the environment for you

Then, you'll be all set up already!

## Running Tests

### Local Tests

Run the following:

```bash
just test # Check out the justfile to see the command this runs
```
This is equivalent to running `pytest` in the root directory of the project.

### Integration Tests

Read the [README.md in the integration folder](./tests/integration/README.md) to see how to run the integration tests.

```bash
just test-i # Check out the justfile to see the command this runs
```

### ZKsync Tests

These will be the ZKsync tests that require the [ZKsync requirements](#zksync-requirements) to be installed. 

```bash
just test-z # Check out the justfile to see the command this runs
```

### Live Tests

A "live test" is sending actual testnet ETH to sepolia. To do this, you'll need:
1. An environment variable `SEPOLIA_ZKSYNC_RPC_URL` set to the sepolia testnet RPC URL
2. A `mox wallet` named `smalltestnet` that has some sepolia ETH
3. A password for your `smalltestnet` wallet in `~/.moccasin/unsafe-passwords/smalltestnet`

Then run:

```bash
uv run pytest tests/live/test_live_verify.py  --no-skip
```

> Note: There is almost no reason to run this test.

# Code Style Guide

We will run the `.github/workflows` before merging your PR to ensure that your code is up to standard. Be sure to run the scripts in there before submitting a PR.

For type checking:

```bash
just typecheck # Check out the justfile to see the command this runs
```

For code formatting: 

```bash
just format # Check out the justfile to see the command this runs
```

## Where do you get the `typecheck` and `format` command?

You can see in `justfile` a list of scripts one can run. To see them all you can run simply `just`

## Editing documentation

User-facing docs live in `docs/source/` (Sphinx), plus root markdown and test READMEs. Before submitting doc changes:

1. Read [docs/STYLE.md](./docs/STYLE.md) for naming and voice conventions.
2. Build locally: `uv sync --extra docs` then `just docs` (or `just docs-watch` while editing).

Do not hand-edit autogenerated files under `docs/source/_autogenerated/`; fix `docs/source/_generate_vars.py` instead. CLI help embedded in the docs comes from Python—change the CLI strings, then rebuild.

# Thank you!

Thank you for wanting to participate with moccasin!