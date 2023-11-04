#We operate our staking infrastructure and also utilize it to support our portfolio investments. 

https://stc.capital/staking 

**Discord: @stccapital**

#Before you start

This guide outlines how to set up an Avail light client on Ubuntu.


![image](https://github.com/trankimly10/Run-Avail-Light-Client-/assets/53910478/6c6ae9fb-8c57-45ec-935d-d1e6408d6367)
# Run-Avail-Light-Client-
 # A.Run the Pre-Built Release

```
sudo apt update
sudo apt install make clang pkg-config libssl-dev build-essential
```
```
mkdir -p ${HOME}/avail-light
```
```
cd avail-light
```
```
wget https://github.com/availproject/avail-light/releases/download/v1.7.2/avail-light-linux-amd64.tar.gz
```
```
tar -xvzf avail-light-linux-amd64.tar.gz
cp avail-light-linux-amd64 avail-light
```
```
./avail-light --network biryani
```
![image](https://github.com/trankimly10/Run-Avail-Light-Client-/assets/53910478/e69f3105-4bc4-46bb-9934-233e785d729b)

** Create Systemd file
** 
```
touch /etc/systemd/system/availd.service
nano /etc/systemd/system/availd.service
```

** put it into Avail service**

```
[Unit] 
Description=Avail Light Client
After=network.target
StartLimitIntervalSec=0
[Service] 
User=root 
ExecStart=${HOME}/avail-light/avail-light --network biryani
Restart=always 
RestartSec=120
[Install] 
WantedBy=multi-user.target

```
**Save it: CTRL+X -- Yes** .


**To enable this to autostart on bootup run:**

```systemctl enable availd.service```

Start it manually with:

```systemctl start availd.service```

You can check that it's working with:

```systemctl status availd.service```

You can tail the logs with journalctllike so:

```journalctl -f -u availd```
![image](https://github.com/trankimly10/Run-Avail-Light-Client-/assets/53910478/b1463796-4124-49b3-9cef-f66f5c3e6165)

#  B. Built from the source:

1. Install Rust

```
sudo apt-get update
sudo apt install build-essential
sudo apt install --assume-yes git clang curl libssl-dev protobuf-compiler
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
source ~/.cargo/env
rustup default stable
rustup update
rustup update nightly
rustup target add wasm32-unknown-unknown --toolchain nightly
```

2. You can run the Avail Light Client using the following command:

```
git clone https://github.com/availproject/avail-light.git
cd avail-light
git checkout v1.7.2
cargo build --release
```
3. Create Systemd file
```
touch /etc/systemd/system/availd.service
nano /etc/systemd/system/availd.service
```

** put it into Avail service**

```
[Unit] 
Description=Avail Light Client
After=network.target
StartLimitIntervalSec=0
[Service] 
User=root 
ExecStart= /root/avail-light/target/release/avail-light --network biryani
Restart=always 
RestartSec=120
[Install] 
WantedBy=multi-user.target

```
**Save it: CTRL+X -- Yes** .


**To enable this to autostart on bootup run:**

```systemctl enable availd.service```

Start it manually with:

```systemctl start availd.service```

You can check that it's working with:

```systemctl status availd.service```

![image](https://github.com/trankimly10/Run-Avail-Light-Client-/assets/53910478/cd0ba0b1-679d-4d12-8ad6-e8a1ae9aa257)

You can tail the logs with journalctllike so:

```journalctl -f -u availd```

![image](https://github.com/trankimly10/Run-Avail-Light-Client-/assets/53910478/b01d6988-5e85-4a5c-a67b-6b24235d5ac3)

