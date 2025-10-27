# Sovereign - Personal Bitcoin Node
last updated: 27th October 2025.

**Bitcoin self-custody and sovereignty is for everyone - no third-party trust required. Free full node guide for non-technical users, regularly maintained and updated.**

[![Watch Intro Video](https://github.com/www-codeblock-io/Sovereign/blob/main/repo_resources/video_intro.png)](https://www.youtube.com/watch?v=lkLX7CVw-Og)

## Disclosure
This guide contains Amazon affiliate links. As an Amazon Associate, I earn from qualifying purchases. This helps support the development and maintenance of this guide at no additional cost to you. All recommendations are based on my personal experience and research.

# Project goal
A cookbook to convert an old laptop into a Sovereign Personal Bitcoin Node.

Easy to follow instructions to build a secure and sovereign Linux based Bitcoin node using free open source software, self-verified (non-branded/containerised), enabling the use of hardware wallets while preserving privacy of personal bitcoin addresses (& balances) when interacting with the bitcoin network.

Because external guides can be out-of-date and not actively maintained. This guide has a subheading stating the last update and a link to each official software project page for further self verification.

Think of this as a general installation guide for non-technical users.

**Need help implementing this guide?** I offer private pseudonymous consultation services for non-technical users. Visit [sovereign101.com/consultation](https://sovereign101.com/consultation) for 1-on-1 expert guidance.

# Why run a bitcoin node?

Inspired by [Arman The Parman](https://armantheparman.com/why-should-you-run-your-own-bitcoin-node/)
with a few personal additions...

1. You can maximise privacy. Connecting your bitcoin wallet to your a node means not relying on someone else's copy of the timechain data, you won't divulge your IP (your location!) nor your bitcoin addresses (and their balances). It's harder for potential attackers to even know you exist and provides protection from surveillance firms who WILL co-operate with your local ruler when it's confiscation time during the inevitable collapse of fiat.

2. You can verify if you have been paid - like checking a gold payment is real by melting it down. A bitcoin payment must register on your copy of the timechain.

3. Defend the rules of your money if there is a contentious fork - no one can force you to run Bitcoin Larry Fink's Vision, for example.

4. Be one of many cockroaches that need to be destroyed to wipe out the UTXO set (who owns what). Note: even that doesn't kill Bitcoin, Bitcoin is an idea. They'd have to kill all the Bitcoiners.

5. Help someone else run a node, or provide the infrastructure so someone else can trust you and connect to your node. Remember, being a human node is not the power to run the software but the power to choose the right software to connect to - you can be that option for people, especially those you orange pill, instead of letting them connect to a random node.

6. Enjoy peace of mind, and gain a greater appreciation for the power of Bitcoin. You'll probably end up buying more, and accumulating more girlfriends.


---
## HARDWARE

Bitcoin Knots [minimum requirements](https://bitcoin.org/en/bitcoin-core/features/requirements)
- Ram: 1GB
- CPU: Some ARM chipsets >1.GHz
- HDD: 650GB (however large the Bitcoin blockchain currently is.)
- Download: 500 MB/day (15 GB/month)
- Upload: 5 GB/day (150 GB/month)

Most entry level laptops should meet the above specifications. Just upgrade the existing HDD to a 2T NVMe SSD card and connect the WiFi to an unlimited broadband connection.

### Recommended Hardware Components

**Laptop**: I purchased this second hand [HP portable laptop](https://amzn.to/40uZ4ZC) from Amazon.com for $140.
- Ram: 16GB
- CPU: Intel celeron 1.1 GHz
- HDD: 64GB

**Storage Upgrade**: At time of writing the Bitcoin blockchain is around 600GB of data so you will almost certainly need to upgrade the laptops internal SSD card. The NVMe SSD I upgraded to was this [2TB SSD card](https://amzn.to/3TUmjIT) for $93.

**USB Drive**: For creating bootable Ubuntu installation media, I recommend using a [32GB USB drive](https://amzn.to/46nhQG8) with good read/write speeds.

---
## SOFTWARE
- Ubuntu 24.04 LTS
- Bitcoin Knots 28.1
- Tor
- Electrs
- Electrum 4.5.8
- Specter Desktop
- Sparrow 2.2.3

(optional)
- ProtonVPN
- Brave Browser
- Telegram Desktop

### Recent Software Updates (July 2025)
- **Bitcoin Knots 28.1.knots20250305: March 2025 with enhanced features, more conservative policies, and additional privacy options compared to Bitcoin Core**
- **Electrum 4.5.8**: Enhanced security patches, Nostr support for submarine swaps, improved stability
- **Sparrow 2.2.3**: Better hardware wallet support (OneKey Pro, Trezor Safe 5, Ledger Stax/Flex), improved QR scanning, enhanced fee management
- **Ubuntu 24.04 LTS**: Latest stable release with support until 2029, improved hardware compatibility

___
## VERIFY & INSTALL SOFTWARE
For all Bitcoin software, it’s a particularly important security step to verify the release. This is done to ensure the installation file you download has not been compromised. Follow download instructions and use gpg in the terminal as instructed.

___
# Install Ubuntu 24.04 LTS
**Estimated time: 30-45 minutes**

I installed Ubuntu 24.04 LTS as it's the latest stable LTS release, providing security updates until 2029.

## Deactivate Secure-Boot
If repurposing an old Windows laptop, Deactivate Secure-Boot.

Secure boot signing authorities have made mistakes in the past ([section 3, page 2 under 'Disadvantages'](https://www.nsa.gov/portals/75/documents/what-we-do/cybersecurity/professional-resources/BootSecurityModesAndRec_20190522.pdf)). Let's verify all the software ourselves and not trust a third-party to do this for us.

1. Press the laptops power-on button then immediatly press the Function key that enters the Bios menu. For the HP Laptop I'm using it was the F2 key. [Bios key by manufacturer. ](https://gadgetmates.com/bios-key-by-manufacturer)
2. Once the system Bios has loaded, proceed to turn-off ```Secure Boot``` (usually located under the ```security``` tab), save and exit. Then turn-off the laptop.

3. On a seperate PC head over to [Ubuntu Releases](https://releases.ubuntu.com/noble/ "Ubuntu releases") and download the following three files: 
   - ```Ubuntu-24.04.4-desktop-amd64.iso```
   - ```SHA256SUMS```
   - ```SHA256SUMS.gpg``` 

   Save all three files to your Downloads folder.


## Verify download signitures
Note, the slightly different commands, depending if you are on Windows or Linux.
[Reference Link](https://ubuntu.com/tutorials/how-to-verify-ubuntu#2-necessary-software "Ubuntu tutorial")

### Windows10
1. Verify signatures:
   ```bash
   gpg --keyid-format long --verify SHA256SUMS.gpg SHA256SUMS.txt
   ```
2. Verify ISO file:
   ```bash
   certutil -hashFile <ISO_file_path> SHA256
   ```
Compare the output with the hash in SHA256SUMS.txt.

### Linux/MacOS
1. Verify signatures:
   ```bash
   gpg --keyid-format long --verify SHA256SUMS.gpg SHA256SUMS.txt
   ```
2. Verify ISO file:
   ```bash
   sha256sum -c SHA256SUMS 2>&1 | grep OK
   ```


## Complete install
Follow the [official](https://ubuntuhandbook.org/index.php/2024/04/install-ubuntu-24-04-desktop/amp/ "https://ubuntuhandbook.org/index.php/2024/04/install-ubuntu-24-04-desktop/amp/")
installation instructions to install Ubuntu.

[Create partition table](https://ubuntu.com/tutorials/install-ubuntu-desktop#3-create-a-bootable-usb-stick "https://ubuntu.com/tutorials/install-ubuntu-desktop#3-create-a-bootable-usb-stick") (not always required).




---
# Tip - Linux keyboard shortcuts.
- Display Desktop: ```WINDOWS KEY+D```
  
- Open a new Terminal window: ```CTRL+ALT+T```

- Copy text in the Terminal: ```CTRL+SHIFT+C```

- Paste text in the Terminal: ```CTRL+SHIFT+P```


---
## Complete Ubuntu Setup
**Estimated time: 15-20 minutes**

Once Ubuntu installation has finished, complete the following setup steps:

### 1. Initial Configuration
```bash
# Update package manager
   sudo apt update && sudo apt upgrade

# Install Git
   sudo apt install git

# Install dependencies for Specter
   sudo add-apt-repository universe && sudo apt install libfuse2
   ```

### 2. Power Management Setup
Because you will want to run your node for 6+ hours a day (24hrs is better), configure power settings:

**GUI Settings:**
- Navigate to: Show Apps > Settings > Power Settings
- Set Power Mode = Balanced
- Set Automatic Power Saver = Off  
- Set Automatic suspend = Off

**Laptop Lid Configuration:**
```bash
# Configure laptop lid to do nothing when closed
sudo nano /etc/systemd/logind.conf
# Uncomment and set: HandleLidSwitch=ignore
   sudo systemctl restart systemd-logind
   ```
*Note: This will log you out of Ubuntu*

___
## 🎯 Progress Checkpoint: Ubuntu Setup Complete!
**You're about 25% done with the setup process.**

# Install Proton VPN
1. Download repo:
   ```bash
   cd ~/Downloads && wget https://repo.protonvpn.com/debian/dists/stable/main/binary-all/protonvpn-stable-release_1.0.4_all.deb
   ```

2. Install repo:
   ```bash
   sudo dpkg -i ./protonvpn-stable-release_1.0.4_all.deb && sudo apt update
   ```

3. Verify package integrity:
   ```bash
   echo "62a9d849835de8a5664cf95329458bf1966780b15cec420bf707b5f7278b9027  protonvpn-stable-release_1.0.4_all.deb" | sha256sum --check -
   ```

4. Install ProtonVPN:
   ```bash
   sudo apt install proton-vpn-gnome-desktop
   ```

6. Update system:
   ```bash
   sudo apt update && sudo apt upgrade
   ```

7. Enable system tray (optional):
   ```bash
   sudo apt install libayatana-appindicator3-1 gir1.2-ayatanaappindicator3-0.1 gnome-shell-extension-appindicator
   ```
8. Clean up:
   ```bash
   cd ~/Downloads && rm -r protonvpn-stable-release_1.0.4_all.deb
   ```
9. Headover to [ProtonVPN](https://account.protonvpn.com/signup "ProtonVPN.com") and Sign-up to a free account.

**_Connect to ProtonVPN whenever accessing a web browser on your machine._**

---
# Install Brave Browser (optional)
1. Install curl:
   ```bash
   sudo apt install curl
   ```
2. Add Brave key:
   ```bash
   sudo curl -fsSLo /usr/share/keyrings/brave-browser-archive-keyring.gpg https://brave-browser-apt-release.s3.brave.com/brave-browser-archive-keyring.gpg
   ```
3. Add repository:
   ```bash
   echo "deb [signed-by=/usr/share/keyrings/brave-browser-archive-keyring.gpg] https://brave-browser-apt-release.s3.brave.com/ stable main"|sudo tee /etc/apt/sources.list.d/brave-browser-release.list
   ```
4. Install Brave:
   ```bash
   sudo apt update && sudo apt install brave-browser
   ```

---
# Install Telegram Desktop (optional)
A quick solution for encrypted files/messages.
1. Install Telegram:
   ```bash
   sudo apt install telegram-desktop
   ```

---
# Install Bitcoin Knots
**Estimated time: 20-30 minutes**

Head over to [Bitcoin Knots](https://bitcoinknots.org/) and:
- Download the latest Linux(tgz) 64 bit version and save to Downloads folder
- Bitcoin Knots is a derivative of Bitcoin Core with enhanced features, more conservative policies, and additional privacy options
- Bitcoin Knots uses the same command-line interface as Bitcoin Core (bitcoin-cli, bitcoin-qt, bitcoind)
- Follow the verification instructions on the Bitcoin Knots website to verify your download using GPG signatures

## Complete install
[Reference Link](https://bitcoin.org/en/full-node#linux-instructions "Bitcoin.org")

1. Extract Bitcoin Knots:
   ```bash
   tar xzf bitcoin-28.1.knots20250305-x86_64-linux-gnu.tar.gz
   ```
2. Install Bitcoin Knots:
   ```bash
   sudo install -m 0755 -o root -g root -t /usr/local/bin bitcoin-28.1.knots20250305/bin/*
   ```
3. Clean up:
   ```bash
   cd ~/Downloads && sudo rm -r bitcoin-28.1.knots20250305-x86_64-linux-gnu.tar.gz SHA256SUMS.asc SHA256SUMS
   ```

---
## Run Bitcoin Knots (start initial blockchain download)
**Estimated time: 3-7 days (initial sync)**

1. Start Bitcoin Knots:
   ```bash
   bitcoin-qt
   ``` 
   You will be greated with the Bitcoin Knots Welcome screen.

2. Uncheck ```Limit block chain storage```. We want to download the complete Bitcoin blockchain from the genisis block.
3. Click ```OK```.

Bitcoin Knots will now create the main ```data-directory``` in a hidden folder .bitcoin inside your home directory. It is here that all Bitcoin Knots configuaration files will be stored along with the complete blockchain data. Get familiar with this ```data-directory``` (home/USERNAME/.bitcoin) location as we will be accessing it again later.

4. Leave the laptop power plugged in and wait for the Bitcoin blockchain to download, Bitcoin Knots will show a % complete and a rough estimate of how much time remains until completion.


---
## Configure Bitcoin Knots
1. Once Bitcoin Knots is fully synced you will be greeted with a welcome screen asking if you would like to ```Create a new wallet```. Proceed to create a standard wallet. 

2. Then edit Bitcoin Knots config file.

3. From the Bitcoin Knots GUI click on ```Settings```, ```Options```, then ```Open Configuration File```.

4. Enter the below text, save and exit
   ```bash
   # server=1, this tells Bitcoin to accept JSON-RPC commands 
   # (such as ones from EPS or Electrs etc.). txindex=1 allows any transaction 
   # to be looked up by EPS, this flag is not required for Electrs.
   server=1
   txindex=1
   listen=1

   proxy=127.0.0.1:9050
   bind=127.0.0.1

   datadir=

   # only connect to Tor hidden services, not even IPv4/IPv6 nodes
   onlynet=onion
  
   # Electrs can use the .cookie setting to connect to Bitcoin Knots
   # but Specter can not and requires the rpcuser/rpcpassword to be set.
   rpcuser=<User>
   rpcpassword=<Password>
   
   # If running tor, walletbroadcast=0 prevents the node from 
   # rebroadcasting transactions without tor.
   walletbroadcast=0
   
5. Now shut down Bitcoin Knots so that the config changes we made can be applied. Click on the ```X``` in the top right hand corner. Or enter the below command in any Terminal window:
   ```bash
   bitcoin-cli stop
   ```
## Allow incoming connections (optional but recommended)
Configure your WIFI router to allow Bitcoin Knots incoming connections on port:8332. Make a note of both your MAC and IP address then follow the instructions in this [Link](https://bitcoin.org/en/full-node#network-configuration)

Retrieve your Laptops MAC address and IP address from the Terminal. 

1. Get MAC address:
   ```bash
   ip link
   ```
   Look for `link/ether=##:##:##:##:##:##` in the output.

2. Get IP address:
   ```bash
   hostname -I
   ```
## Some other helpful commands
3. Install net-tools:
   ```bash
   sudo apt install net-tools
   ```
4. Check Bitcoin connections:
   ```bash
   sudo netstat --ip -lpa|grep bitcoin
   ```

## Switching Between Bitcoin Core and Bitcoin Knots

You can easily switch between Bitcoin Core and Bitcoin Knots:
- Both use the same data directory (~/.bitcoin)
- Both use identical configuration files
- Simply install the other version and replace the binaries
- No need to re-download the blockchain
  
---
# Install Tor
**Estimated time: 10-15 minutes**
**Last updated: July 2025**
[Official website](https://support.torproject.org/apt/tor-deb-repo/)

"Browse Privately. Explore Freely.
Defend yourself against tracking and surveillance. Circumvent censorship." - Torproject.org

1. Check CPU architecture:
   ```bash
   dpkg --print-architecture
   ```
2. Install apt-transport-https:
   ```bash
   sudo apt install apt-transport-https
   ```
3. Check Linux distribution:
   ```bash
   lsb_release -c
   ```
4. Create Tor repository file:
   ```bash
   cd /etc/apt/sources.list.d/
   ```
5. Edit tor.list:
   ```bash
   sudo nano tor.list
   ```
6. Add repository entries:
   ```bash
   deb     [arch=amd64 signed-by=/usr/share/keyrings/deb.torproject.org-keyring.gpg] https://deb.torproject.org/torproject.org noble main
   deb-src [arch=amd64 signed-by=/usr/share/keyrings/deb.torproject.org-keyring.gpg] https://deb.torproject.org/torproject.org noble main
   ```
7. Add Tor GPG key:
   ```bash
   sudo wget -qO- https://deb.torproject.org/torproject.org/A3C4F0F979CAA22CDBA8F512EE8CBC9E886DDD89.asc | gpg --dearmor | sudo tee /usr/share/keyrings/deb.torproject.org-keyring.gpg >/dev/null
   ```
8. Update package list:
   ```bash
   sudo apt update
   ```
9. Install Tor:
   ```bash
   sudo apt install tor deb.torproject.org-keyring
   ```
10. Verify installation:
    ```bash
    tor --version
    ```
11. Enable auto-start (optional):
    ```bash
    sudo systemctl enable tor
    ```

## Tor Systemctl commands
1. Restart Tor:
   ```bash
   sudo systemctl restart tor
   ```
2. Check status:
   ```bash
   sudo systemctl status tor
   ```

---
## Set up Tor hidden service
Configure Bitcoin Knots to only connect using Tor. [Reference link](
https://en.bitcoin.it/wiki/Setting_up_a_Tor_hidden_service)

Additional video tutorial, for further reference: [Canadian Bitcoiners](
https://www.youtube.com/watch?v=goTkOt8Rr1Q&list=PLZqQw4mLW-r3UEyL12FG4koZq6lOLsURF&index=3)

1. Edit Tor config:
   ```bash
   cd /etc/tor
   ```
2. Edit torrc:
   ```bash
   sudo nano torrc
   ```
3. Add configuration:
   ```bash
   ControlPort 9051
   CookieAuthentication 1
   CookieAuthFileGroupReadable 1
   ```
4. Find Bitcoin user:
   ```bash
   ps -eo user,group,comm |egrep 'bitcoind|bitcoin-qt' |awk '{print "Bitcoin user: " $1}'
   ```
5. Add user to Tor group:
   ```bash
   sudo usermod -a -G debian-tor <user name found from above command>
   ```
6. Check Tor groups (if needed):
   ```bash
   getent group
   ```
   
The above configuration sets up an automatic hidden service that is initiated by Bitcoin Knots. On the next startup of bitcoin, Bitcoin Knots will generate a file called ```onion_private_key``` in the data directory. KEEP THIS SAFE. If someone copies this file they can run a server with your .onion address. While a malicious party cannot necessarily associate the server with you as a person, as long as your server has the same xxxx.onion address they will know it is run by the same person.

If you delete this file, the next time bitcoind loads it will generate a new key file and xxxxxxxx.onion address.  For absolute security delete your ```onion_private_key``` file at each reboot or some frequent interval.

7. Do a system Restart
   ```bash
   sudo shutdown -r now
   ```

## Verify Bitcoin Knots is using Tor
1. Verify Tor connection:
   ```bash
   bitcoin-cli getnetworkinfo
   ```
2. Look for the networks section in the output. Your node is running behind Tor if you see these settings:
   ```
   "name": "ipv4",
         "limited": true,
         "reachable": false

   And

   "name": "onion",
         "limited": false,
         "reachable": true
   ```
   This confirms that IPv4 is disabled and only Tor (onion) connections are active.


---
## 🎯 Progress Checkpoint: Bitcoin Node Running!
**You're about 50% done with the setup process.**

# Install Electrs
**Estimated time: 45-60 minutes (build time)**
[Official website](https://github.com/romanz/electrs/tree/master?tab=readme-ov-file)

"Electrs is a great low-resource, easy-to-install option for personal use - especially on resource-constrained hardware." - [Jameson Lopp](https://blog.casa.io/electrum-server-performance-report/)

## Build dependencies
1. Install Rust:
   ```bash
   curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
   ```
2. Install Cargo:
   ```bash
   sudo apt install cargo
   ```
3. Update packages:
   ```bash
   sudo apt update
   ```
4. Install build tools:
   ```bash
   sudo apt install clang cmake build-essential
   ```

I chose to compile electrs by statically linking to librocksdb, which has less dependencies.

5. Install RocksDB dependencies:
   ```bash
   sudo apt install -y libgflags-dev libsnappy-dev zlib1g-dev libbz2-dev liblz4-dev libzstd-dev
   ```
6. Clone RocksDB:
   ```bash
   git clone -b v7.8.3 --depth 1 https://github.com/facebook/rocksdb && cd rocksdb
   ```
7. Build and install:
   ```bash
   make shared_lib -j $(nproc) && sudo make install-shared
   ```
8. Clean up:
   ```bash
   cd .. && rm -r rocksdb
   ```
9. Install cfg_me (optional):
   ```bash
   cargo install cfg_me
   ```
10. Clone Electrs:
    ```bash
    cd ~ && git clone https://github.com/romanz/electrs
    ``` 
11. Enter directory:
    ```bash
    cd electrs
    ```
## Build Electrs

12. Build Electrs (~20 minutes):
    ```bash 
    cargo build --locked --release
    ```
    During installation build the below warning was thrown:

    ```bash
    warning: electrs (lib) generated 1 warning (run cargo fix --lib -p electrs to apply 1 suggestion)
    Finished release [optimized] target(s) in 5m 53s
    ```

    If you see warnings, run:
    ```bash
    cargo fix --lib -p electrs
    ```

---
## Configure Electrs
1. Create symbolic link:
   ```bash
   sudo ln -s /home/<USER>/electrs/target/release/electrs /usr/local/bin/electrs
   ```
2. Verify link:
   ```bash
   ls -l /usr/local/bin
   ```

3. Test installation:
   ```bash
   electrs --version
   ```
     
4. Create config:
   ```bash
   cd ~ && sudo mkdir .electrs && sudo nano .electrs/config.toml   
   ```
5. Copy below text into config.toml, save and exit
   ```bash
   # DO NOT EDIT THIS FILE DIRECTLY - COPY IT FIRST!
   # If you edit this, you will cry a lot during update and will not want to live anymore!
   
   # This is an EXAMPLE of how configuration file should look like.
   # Do NOT blindly copy this and expect it to work for you!
   # If you don't know what you're doing consider using automated setup or ask an experienced friend.
   
   # This example contains only the most important settings.
   # See docs or electrs man page for advanced settings.

   # Use the below auth="USER:PASSWORD if you have RPC user:password set/active
   # in bitcoin.conf file.
   auth="<User>:<Password>"

   # The listening RPC address of bitcoind, port is usually 8332
   daemon_rpc_addr = "127.0.0.1:8332"
   
   # The listening P2P address of bitcoind, port is usually 8333
   daemon_p2p_addr = "127.0.0.1:8333"
   
   # Directory where the index should be stored. It should have at least 70GB of free space.
   db_dir = "/home/<User>/electrs/db"
   
   # bitcoin means mainnet. Don't set to anything else unless you're a developer.
   network = "bitcoin"
   
   # The address on which electrs should listen. Warning: 0.0.0.0 is probably a bad idea!
   # Tunneling is the recommended way to access electrs remotely.
   electrum_rpc_addr = "127.0.0.1:50001"
   
   # How much information about internal workings should electrs print. Increase before reporting a bug.
   log_filters = "INFO"

   ```
## Build Electrs server index
6. Check Bitcoin data size:
   ```bash
   du -ch ~/.bitcoin/blocks/blk*.dat | tail -n1
   ```
   This will print the size of the existing Bitcoin Knots block directory. The final Electrs index DB will be about 10-20% the size of the Bitcoin Knots block directory.

7. Start Bitcoind and wait for bitcoind to complete initial sync.
   ```bash
   bitcoind -server -daemon
   ```

8. Check sync status:
   ```bash
   bitcoin-cli getblockchaininfo | head
   ```
   
9. Start Electrs initial sync. **First sync can take 1-2 days depending on CPU/hardware.**
   ```bash
   electrs --log-filters INFO
   ```
10. Check Electrs DB size:
   ```bash
   du ~/electrs/db
   ```
---
## 🎯 Progress Checkpoint: Electrs Indexed!
**You're about 75% done with the setup process.**

# Install all three Bitcoin wallets: Electrum, Sparrow & Specter
**Estimated time: 30-45 minutes**

## Prerequisites
- Bitcoin Knots must be running and synced
- Electrs must be running and indexed
- Wait for `INFO electrs::chain chain updated` before starting wallets

## Electrum Wallet
[Official website](https://electrum.org/#download)

**Installation:**
```bash
# Download and verify
cd ~/Downloads
wget https://raw.githubusercontent.com/spesmilo/electrum/master/pubkeys/ThomasV.asc && gpg --import ThomasV.asc
   sudo apt-get install python3-pyqt5 libsecp256k1-dev python3-cryptography
   wget https://download.electrum.org/4.5.8/Electrum-4.5.8.tar.gz
   wget https://download.electrum.org/4.5.8/Electrum-4.5.8.tar.gz.asc && gpg --verify Electrum-4.5.8.tar.gz.asc
   sudo apt-get install python3-setuptools python3-pip && python3 -m pip install --user Electrum-4.5.8.tar.gz
   cd ~/Downloads && sudo rm -r Electrum-4.5.8.tar.gz Electrum-4.5.8.tar.gz.asc ThomasV.asc
   ```

**Configuration:**
```bash
# Launch with Tor settings
   electrum --oneserver --server 127.0.0.1:50001:t --proxy socks5:127.0.0.1:9150
   ```
 
**Close Electrum immediately, then edit config:**
```bash
   cd ~/.electrum && nano config
   ```

**Config file contents:**
```json
   {
       "auto_connect": false,
       "check_updates": false,
       "decimal_point": 8,
       "log_to_file": true, 
       "oneserver": true,
       "proxy": "socks4:localhost:9050",
       "proxy_password": "",
       "proxy_user": "",
       "server": "localhost:50001:t"
   }
   ```

## Specter Desktop
[Official Website](https://specter.solutions/index.html)

**Installation:**
```bash
# Install Python 3.10 and Specter
sudo apt install software-properties-common
sudo add-apt-repository ppa:deadsnakes/ppa
sudo apt update
sudo apt install python3.10 python3.10-venv python3.10-dev python3-venv
python3.10 -m venv ~/.specter-env
source ~/.specter-env/bin/activate
pip install --upgrade pip
pip install cryptoadvance.specter
pip uninstall cryptoadvance-spectrum -y
```

**Configuration:**
- Start Bitcoin Knots: `bitcoind -daemon`
- Start Specter: `python -m cryptoadvance.specter server --host 127.0.0.1 --port 25442`
- Open browser: `http://127.0.0.1:25442`
- Connect to Bitcoin Knots: Host=127.0.0.1, Port=8332, Username/Password from bitcoin.conf

## Sparrow Wallet
[Official Website](https://sparrowwallet.com/)

**Installation:**
```bash
# Download and verify
wget https://keybase.io/craigraw/pgp_keys.asc | gpg --import
wget https://sparrowwallet.com/download/sparrow-2.2.3-manifest.txt.asc && gpg --verify sparrow-2.2.3-manifest.txt.asc
wget https://sparrowwallet.com/download/sparrow-2.2.3-manifest.txt && sha256sum --check sparrow-2.2.3-manifest.txt --ignore-missing
sudo dpkg -i sparrow_2.2.3-1_amd64.deb
```

**Configuration:**
- Server type: Private Electrum
- URL: 127.0.0.1:50001
- Use SSL: Off
- Use Proxy: On (127.0.0.1:9050)

## Verification
If the Network light in the bottom right corner of any wallet is blue, you're connected to your own node running behind Tor. It's now safe to interact with your real wallets.

---
# Desktop Configuration

## Create Desktop Icons

### General Process
1. **Create executable script**: `nano ~/app-name.sh`
2. **Download icon**: `wget [icon-url]` to `~/.icons/`
3. **Create .desktop file**: `nano ~/app-name.desktop`
4. **Make executable**: `chmod +x ~/app-name.desktop`
5. **Move to desktop**: `mv ~/app-name.desktop ~/Desktop/`
6. **Enable launching**: Right-click icon → "Allow Launching"

### Bitcoin Node Desktop Icon
**Script content** (`~/node.sh`):
```bash
#!/bin/bash
/usr/local/bin/bitcoind &
sleep 5
/usr/local/bin/electrs --log-filters INFO
exit 0
```

**Desktop file** (`~/bitcoin.desktop`):
```ini
[Desktop Entry]
Version=1.0
Type=Application
Terminal=true
Icon=btclogo
Name=Bitcoin
Exec=/home/<user>/node.sh
Comment=Launch Bitcoin Node
```

**Icon setup**:
```bash
mkdir -p ~/.icons
cd ~/.icons && wget https://bitcoin.design/assets/images/guide/getting-started/visual-language/bitcoin-symbol.svg
mv bitcoin-symbol.svg btclogo.svg
```

### Electrum Desktop Icon
**Desktop file** (`~/electrum.desktop`):
```ini
[Desktop Entry]
Name=Electrum
Comment=Lightweight Bitcoin Wallet
GenericName=Bitcoin Wallet
Exec=/home/<USER>/.local/bin/electrum
Icon=electrum
Type=Application
```

**Icon setup**:
```bash
# Electrum uses the built-in icon, no additional setup needed
# The icon=electrum in the desktop file references the system icon
```

### Specter Desktop Icon
**Script content** (`~/start-specter-desktop.sh`):
```bash
#!/bin/bash
# Function to check if Specter is already running
check_specter() {
    if lsof -Pi :25442 -sTCP:LISTEN -t >/dev/null 2>&1; then
        return 0  # Specter is running
    else
        return 1  # Specter is not running
    fi
}

# Check if Specter is already running
if check_specter; then
    echo "Specter is already running, opening browser..."
    brave-browser http://127.0.0.1:25442
    exit 0
fi

# Start Specter server
echo "Starting Specter server..."
cd ~
source ~/.specter-env/bin/activate

# Start Specter in background
nohup python -m cryptoadvance.specter server --host 127.0.0.1 --port 25442 > ~/.specter/specter.log 2>&1 &

# Wait for server to start
echo "Waiting for Specter to start..."
for i in {1..10}; do
    if check_specter; then
        echo "Specter started successfully!"
        sleep 2
        brave-browser http://127.0.0.1:25442
        exit 0
    fi
    sleep 1
done

echo "Failed to start Specter server. Check ~/.specter/specter.log for errors."
exit 1
```

**Desktop file** (`~/specter.desktop`):
```ini
[Desktop Entry]
Version=1.0
Type=Application
Terminal=true
Icon=/home/<USER>/.icons/specter-logo.png
Name=Specter Desktop
Exec=/home/<USER>/start-specter-desktop.sh
Comment=Bitcoin wallet with hardware wallet support
```

**Icon setup**:
```bash
# Download Pacman icon for Specter
wget https://www.freeiconspng.com/download/25184 -O ~/Downloads/pacman-png-25184.png
mv ~/Downloads/pacman-png-25184.png ~/.icons/specter-logo.png
chmod 644 ~/.icons/specter-logo.png
chmod +x ~/start-specter-desktop.sh
```

### Remove Home Folder Icon
    ```bash
  gsettings set org.gnome.shell.extensions.ding show-home false
  ```

---
## Support & Consultation

### Free Resources
- This guide is completely free and open source
- All software mentioned is free and open source
- Community support available through GitHub issues

### Professional Consultation
If you need personalized help implementing this guide, I offer private consultation services:

**Services Available:**
- **Quick Review & Troubleshooting ($500/hour)** - 1-hour troubleshooting session
- **Complete Sovereign Setup ($10,000/session)** - 2-3 hour comprehensive setup
- **Enterprise-Grade Configuration ($12,500/session)** - 3-4 hour advanced setup

**Benefits:**
- 1-on-1 expert guidance
- Non-technical user friendly
- Privacy-focused (no personal details required)
- Bitcoin payments accepted
- 30-day follow-up support

**Book Consultation:** [sovereign101.com/consultation](https://sovereign101.com/consultation)

*This consultation service helps support the continued development and maintenance of this free guide.*

---

