# Wrapper for Balance of Satoshis

`balanceofsatoshis` is a Command Line tool for working with LND balances. This is considered a Power User LND Tool, and is not officially supported by Start9.

## Dependencies

- [docker](https://docs.docker.com/get-docker)
- [docker-buildx](https://docs.docker.com/buildx/working-with-buildx/)
- [yq](https://mikefarah.gitbook.io/yq)
- [toml](https://crates.io/crates/toml-cli)
- [embassy-sdk](https://github.com/Start9Labs/embassy-os/tree/master/backend)
- [make](https://www.gnu.org/software/make/)

## Build enviroment
Prepare your EmbassyOS build enviroment. In this example we are using Ubuntu 20.04.

1. Install docker
```
curl -fsSL https://get.docker.com -o- | bash
sudo usermod -aG docker "$USER"
exec sudo su -l $USER
```
2. Set buildx as the default builder
```
docker buildx install
docker buildx create --use
```
3. Enable cross-arch emulated builds in docker
```
docker run --privileged --rm linuxkit/binfmt:v0.8
```
4. Install yq
```
sudo snap install yq
```
5. Install essentials build packages
```
sudo apt-get install -y build-essential openssl libssl-dev libc6-dev clang libclang-dev ca-certificates
```
6. Install Rust
```
curl https://sh.rustup.rs -sSf | sh
# Choose nr 1 (default install)
source $HOME/.cargo/env
```
7. Install toml
```
cargo install toml-cli
```
8. Build and install embassy-sdk
```
cd ~/ && git clone https://github.com/Start9Labs/embassy-os.git
cd embassy-os/backend/
./install-sdk.sh
```

## Cloning

Clone the project locally. Note the submodule link to the original project(s). 

```
git clone https://github.com/Start9Labs/balanceofsatoshis-wrapper.git
cd balanceofsatoshis-wrapper
git submodule update --init --recursive
```
## Building

To build the project, run the following commands:

```
make
```

## Installing (on Embassy)

SSH into an Embassy device.
`scp` the `.s9pk` to any directory from your local machine.
Run the following command to install the package:

```
embassy-cli auth login
#Enter your embassy password then run:
embassy-cli package install /path/to/balanceofsatoshis.s9pk
```
## Verify Install

Go to your Embassy Services page, select Balance of Satoshis and start the service.

# Done
