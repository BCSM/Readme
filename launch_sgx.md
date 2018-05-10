# How to Launch BCSM-SGX

To launch and test BCSM-SGX, a reader needs to follow these steps.

The only operating system that has been tested is Ubuntu 16.04.1.

## Starts an Intel SGX runtime environment

* **Step 1:** Configure the BIOS setting to enable Intel SGX feature of the CPU.
* **Step 2:** Download the Intel SGX Driver & SDK **2.0** for Linux from [here](https://01.org/intel-software-guard-extensions/downloads).
```
wget https://download.01.org/intel-sgx/linux-2.0/sgx_linux_x64_driver_eb61a95.bin
chmod 0777 ./sgx_linux_x64_driver_eb61a95.bin
sudo ./sgx_linux_x64_driver_eb61a95.bin
wget https://download.01.org/intel-sgx/linux-2.0/sgx_linux_ubuntu16.04.1_x64_sdk_2.0.100.40950.bin
chmod 0777 ./sgx_linux_ubuntu16.04.1_x64_sdk_2.0.100.40950.bin
sudo ./sgx_linux_ubuntu16.04.1_x64_sdk_2.0.100.40950.bin
```
* **Step 3:** Remember to `source` the environment variables of the Intel SGX SDK. If this step is missing, BCSM_SGX cannot initialize an enclave.
```
source ./sgxsdk/environment
```
## Pulls the Baidu Rust SGX image

Runs
```
sudo docker pull baiduxlab/sgx-rust
```

## Git clones BCSM-SGX and runs

Clones [BCSM-SGX](https://github.com/huyuncong/BCSM_SGX) and initialize the sub-module.
```
git clone https://github.com/huyuncong/BCSM_SGX.git
cd BCSM_SGX
git submodule init
git submodule update
chmod 0777 run.sh
sudo ./run.sh
```

## Inside SGX

First, we need to run AESM service:
```
/opt/intel/sgxpsw/aesm/aesm_service &
```

We enter the BCSM-SGX, which is in the sample code, and make.
```
cd sgx/samplecode/BCSM_SGX
make
cd bin
./app 1>OUTPUT 2>LOG
```
