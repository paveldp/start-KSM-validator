# start-KSM-validator
guide 11.2023

sudo adduser NAME _USER\
sudo usermod -aG sudo NAME_USER\
sudo apt update && sudo apt upgrade -y\
sudo apt install make clang pkg-config libssl-dev build-essential ntp p7zip-full\
sudo apt-get install protobuf-compiler\

#Install Rust\
curl https://sh.rustup.rs -sSf | sh\
rustup update\
rustup target add wasm32-unknown-unknown   \
git clone https://github.com/paritytech/polkadot-sdk.git\
cd polkadot-sdk/polkadot\
git tag -l | sort -V\
git checkout v1.4.0\
cargo build --release\

 sudo nano /etc/systemd/system/ksm-validator.service

[Unit]\
Description=kusama KSM Validator\
[Service]\
User=NAME _USER\
Group=kusama\
WorkingDirectory=/home/NAME _USER/polkadot-sdk\
ExecStart=/home/NAME _USER/polkadot-sdk/target/release/polkadot \ \
 --validator --database=rocksdb \ \
 --pruning 1000 --chain kusama \ \
 --telemetry-url 'wss://telemetry.polkadot.io/submit/ 1' \ \
 --telemetry-url 'wss://telemetry-backend.w3f.community/submit 1' \ \
 --port 30333 --rpc-port 9933 --name "NAME_Validator"\
Restart=always\
RestartSec=120\
[Install]\
WantedBy=multi-user.target
 
sudo systemctl enable ksm-validator.service\
 sudo systemctl daemon-reload && sudo systemctl restart ksm-validator.service && journalctl -u ksm-validator.service -f -n 100
