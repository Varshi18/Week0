# RISC-V Reference SoC Tapeout Program (VSD)

<div align="center">

[![RISC-V](https://img.shields.io/badge/RISC--V-SoC%20Tapeout-lightgrey?style=for-the-badge\&logo=riscv)](https://riscv.org/)
[![VSD](https://img.shields.io/badge/VSD-Program-lightgrey?style=for-the-badge)](https://vsdiat.vlsisystemdesign.com/)

</div>

This repository documents my progress in the **SoC Tapeout Program by VSD**. The goal is to set up an environment with open-source tools required for digital design, verification, and layout, and then move step by step from RTL to GDSII.

---

## Week 0 — Environment Setup and Tools

| Task                      | Description                                                                             | Status    |
| ------------------------- | --------------------------------------------------------------------------------------- | --------- |
| [Task 0](Week0/README.md) | Installed and verified tools (Yosys, Icarus Verilog, GTKWave, Ngspice, Magic, OpenLANE) | Completed |

---

### System Requirements

* RAM: 6 GB or more
* Disk space: 50 GB free
* OS: Ubuntu 20.04 or higher
* CPU: 4 vCPU

---

### Tools Installed

#### Yosys (Logic Synthesis)

```bash
sudo apt-get update
git clone https://github.com/YosysHQ/yosys.git
cd yosys
sudo apt install make build-essential clang bison flex \
    libreadline-dev gawk tcl-dev libffi-dev git \
    graphviz xdot pkg-config python3 libboost-system-dev \
    libboost-python-dev libboost-filesystem-dev zlib1g-dev
make config-gcc
git submodule update --init --recursive
make
sudo make install
```

#### Icarus Verilog (Simulation)

```bash
sudo apt-get update
sudo apt-get install iverilog
```

#### GTKWave (Waveform Viewer)

```bash
sudo apt-get update
sudo apt-get install gtkwave
```

#### Ngspice (Analog Simulation)

```bash
tar -zxvf ngspice-37.tar.gz
cd ngspice-37
mkdir release && cd release
../configure --with-x --with-readline=yes --disable-debug
make
sudo make install
```

#### Magic (Layout Tool)

```bash
sudo apt-get install m4 tcsh csh libx11-dev tcl-dev tk-dev \
    libcairo2-dev mesa-common-dev libglu1-mesa-dev libncurses-dev
git clone https://github.com/RTimothyEdwards/magic
cd magic
./configure
make
sudo make install
```

#### OpenLANE (Digital Flow)

```bash
sudo apt-get update && sudo apt-get upgrade
sudo apt install -y build-essential python3 python3-venv python3-pip make git \
    apt-transport-https ca-certificates curl software-properties-common

# Docker setup
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o \
    /usr/share/keyrings/docker-archive-keyring.gpg
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] \
    https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | \
    sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io
sudo usermod -aG docker $USER
sudo reboot

# Clone and build
cd $HOME
git clone https://github.com/The-OpenROAD-Project/OpenLane
cd OpenLane
make
make test
```

---

### Key Points

* Completed installation of all required open-source EDA tools.
* Verified tool functionality with sample runs.
* Environment is ready for RTL to GDSII flow in upcoming tasks.

---

## Acknowledgment

Thanks to **Kunal Ghosh** and the **VSD team** for leading this program, and to **RISC-V International**, **ISM**, **VSI**, and **Efabless** for supporting this open-source silicon initiative.

---

### References

* [VSD Program Website](https://vsdiat.vlsisystemdesign.com/)
* [RISC-V International](https://riscv.org/)
* [Efabless Platform](https://efabless.com/)
