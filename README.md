# Sovereign - Personal Bitcoin Node
last updated: 18th July 2025.

**Bitcoin self-custody and sovereignty is for everyone - no third-party trust required. Free full node guide for non-technical users, regularly maintained and updated.**

[![Watch Intro Video](https://github.com/www-codeblock-io/Sovereign/blob/main/repo_resources/video_intro.png)](https://www.youtube.com/watch?v=lkLX7CVw-Og)

## Disclosure
This guide contains Amazon affiliate links. As an Amazon Associate, I earn from qualifying purchases. This helps support the development and maintenance of this guide at no additional cost to you. All recommendations are based on my personal experience and research.

# Project goal
A cookbook to convert an old laptop into a Sovereign Personal Bitcoin Node.

Easy to follow instructions to build a secure and sovereign Linux based Bitcoin node using free open source software, self-verified (non-branded/containerised), enabling the use of hardware wallets while preserving privacy of personal bitcoin addresses (& balances) when interacting with the bitcoin network.

Because external guides can be out-of-date and not actively maintained. This guide has a subheading stating the last update and a link to each official software project page for further self verification.

Think of this as a general installation guide with additional trouble shooting tips.

**Need help implementing this guide?** I offer private anonymous consultation services for non-technical users. Visit [sovereign101.com/consultation](https://sovereign101.com/consultation) for 1-on-1 expert guidance.

# Why run a bitcoin node?

Inspired by [Arman The Parman](https://armantheparman.com/why-should-you-run-your-own-bitcoin-node/)
with a few personal additions...

1. You can maximise privacy. Connecting your bitcoin wallet to your a node means not relying on someone else's copy of the timechain data, you won't divulge your IP (your location!) nor your bitcoin addresses (and their balances). It's harder for potential attackers to even know you exist and provides protection from surveillance firms who WILL co-operate with your local ruler when it's confiscation time during the inevitable collapse of fiat.

2. You can verify if you have been paid - like checking a gold payment is real by melting it down. A bitcoin payment must register on your copy of the timechain.

3. Defend the rules of your money if there is a contentious fork - no one can force you to run Bitcoin Larry Fink's Vision, for example.

4. Be one of many cockroaches that need to be destroyed to wipe out the UTXO set (who owns what). Note: even that doesn't kill Bitcoin, Bitcoin is an idea. They'd have to kill all the Bitcoiners.

5. Help someone else run a node, or provide the infrastructure so someone else can trust you and connect to your node. Remember, being a human node is not the power to run the software but the power to choose the right software to connect to - you can be that option for people, especially those you orange pill, instead of letting them connect to a random node.

6. Enjoy peace of mind, and gain a greater appreciation for the power of Bitcoin. You’ll probably end up buying more, and accumulating more girlfriends.


---
## Need Help? Get Expert Consultation

**Struggling with the setup?** I offer private 1-on-1 consultation to help you implement your sovereign Bitcoin node.

### Consultation Services

- **Quick Setup Review ($150/hour)** - Troubleshooting existing setup, hardware compatibility issues, quick configuration fixes
- **Full Node Implementation ($300/session)** - Complete guided setup including hardware preparation, Ubuntu installation, Bitcoin Knots setup, and wallet configuration
- **Advanced Configuration ($450/session)** - Lightning Network setup, Tor integration, advanced security features, and performance optimization

### Why Choose Consultation?

- **Non-technical friendly** - Perfect for users who find GitHub guides overwhelming  
- **Privacy guaranteed** - No personal details required, anonymous consultation available  
- **Proven track record** - Built by the same person who created this Sovereign guide  
- **Bitcoin payments** - Support the Bitcoin ecosystem with Bitcoin payments  
- **30-day support** - Follow-up assistance included with all sessions  

### Book Your Session

Visit [sovereign101.com/consultation](https://sovereign101.com/consultation) to book your consultation session.

**Value Proposition:** I solved the Bitcoin node setup problem that non-technical people face, and open-sourced the complete solution. Need help implementing it? I offer private consultation - no personal details required.


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
- ProtonVPN
- Electrs
- Electrum 4.5.8
- Specter Desktop
- Sparrow 2.2.3

(optional)
- Brave Browser
- Mullvad VPN
- Telegram Desktop
- Ledger Live

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
1. Verify signitures. Open a Terminal window (CTRL+ALT+T). Run:
   ```bash copy
   gpg --keyid-format long --verify SHA256SUMS.gpg SHA256SUMS.txt
   ```
2. Verify ISO file
   ```bash copy
   certutil -hashFile <ISO_file_path> SHA256
   ```
Now open the SHA256SUMS.txt file in your Downloads folder and compare the SHA256 checksum inside the file with the checksum that was printed to the Terminal. It will be a long hash, verify both hashes/numbers match, if so, your ISO download is authentic.

### Linux/MacOS
1. Verify signitures. Open a Terminal window (CTRL+ALT+T). Run:
   ```bash copy
   gpg --keyid-format long --verify SHA256SUMS.gpg SHA256SUMS.txt
   ```
2. Verify ISO file
   ```bash copy
   sha256sum -c SHA256SUMS 2>&1 | grep OK
   ```
   The output you want will look similar to the following:
      ```ubuntu-24.04.4-desktop-amd64.iso: OK```


## Complete install
Follow the [official](https://ubuntuhandbook.org/index.php/2024/04/install-ubuntu-24-04-desktop/amp/ "https://ubuntuhandbook.org/index.php/2024/04/install-ubuntu-24-04-desktop/amp/")
installation instructions to install Ubuntu.

[Create partition table](https://ubuntu.com/tutorials/install-ubuntu-desktop#3-create-a-bootable-usb-stick "https://ubuntu.com/tutorials/install-ubuntu-desktop#3-create-a-bootable-usb-stick") (not always required).


## Reusing bootable USB
Flashing a USB drive with an ISO image will place a write protection on the USB drive, to prevent accidental deletion of your bootable USB drive data. If you make a mistake and need to reformat the USB drive then use something like [Aomei](https://www.aomeitech.com/download.html#pa "Aomitech.com") to remove the write protection so you can reformat the drive and start again (or to reclaim the USB drive to be used for something else).


---
# Tip - Linux keyboard shortcuts.
- Display Desktop: ```WINDOWS KEY+D```
  
- Open a new Terminal window: ```CTRL+ALT+T```

- Copy text in the Terminal: ```CTRL+SHIFT+C```

- Paste text in the Terminal: ```CTRL+SHIFT+P```


---
## Configure Ubuntu
Once Installation has finished.
1. Update package manager. Run:
   ```bash copy
   sudo apt update && sudo apt upgrade
   ```

## Install Git
1. Install Git
   ```bash copy
   sudo apt install git
   ```

## Install Libfuse
[Official website](https://github.com/AppImage/AppImageKit/wiki/FUSE)

Ubuntu 24.04 LTS dependencies to run Specter and Ledger-Live apps.
1. Install libfuse2
   ```bash copy
   sudo add-apt-repository universe && sudo apt install libfuse2
   ```

## Install AppImageLauncher
Creats Desktop icons to launch AppImages such as Specter & Ledger-Live.
1. Install dependencies  
   ```bash copy
   sudo apt install software-properties-common
   ```
2. Add to apt repo
   ```bash copy
   sudo add-apt-repository ppa:appimagelauncher-team/stable
   ```
3. Update apt  
   ```bash copy  
   sudo apt update
   ```
4. Install
   ```bash copy  
   sudo apt install appimagelauncher
   ```

When first run you will be greeted with ```Welcome to AppImageLauncher!```. Configure your App image prefernces to create a new directory to store your (AppImage) Applications, the default location is: /home/<user>/Applications. Change the location if you wish (I chose the default) then click ```OK```. 

Whenever you run a new AppImage you will have two choices, ```Run Once``` or ```Integrate and run```. Click ```Integrate and run```. This will add an executable icon of the app to your ```App``` folder. You can now also right click the App and add it to your favourites tray on your desktop toolbar. 

## Adjust the power settings
Because you will want to run your node for 6+ hours a day (24hrs is better) you will need to adjust the power & lid closure settings to prevent the laptop entering into a low power mode, slowing or halting network traffic.

### Navigate to the Ubuntu power settings menu:
Show Apps > Settings > Power Settings.

Make the following adjustments:
- Power Mode = Balanced
- Automatic Power Saver = Off
- Automatic suspend = Off

Then close the settings menu.

## Laptop lid, do nothing when closed
1. Navigate to systemd directory. Run:
   ```bash copy
   cd /etc/systemd
   ```
2. Open logind configuration file 
   ```bash copy
   sudo nano logind.conf
   ```
3. Uncomment ```HandleLidSwitch``` and make it equal to ```HandleLidSwitch=ignore```, save and exit.
   

4. Restart the systemd daemon (be aware that this will log you out of Ubuntu) with this command
   ```bash copy
   sudo systemctl restart systemd-logind
   ```

___
# Install Proton VPN
1. Move to Downloads folder and download repo. Run:
   ```bash copy
   cd ~/Downloads && wget https://repo.protonvpn.com/debian/dists/stable/main/binary-all/protonvpn-stable-release_1.0.4_all.deb
   ```

2. Install repo
   ```bash copy
   sudo dpkg -i ./protonvpn-stable-release_1.0.4_all.deb && sudo apt update
   ```

3. Check the repo package integrity by checking its checksum
   ```bash copy
   echo "62a9d849835de8a5664cf95329458bf1966780b15cec420bf707b5f7278b9027  protonvpn-stable-release_1.0.4_all.deb" | sha256sum --check -
   ```

4. Install ProtonVPN desktop app
   ```bash copy
   sudo apt install proton-vpn-gnome-desktop
   ```

6. Check for updates to ensure you’re running the latest version
   ```bash copy
   sudo apt update && sudo apt upgrade
   ```

7. Linux system tray icon (optional)
   By default, GNOME doesn’t support tray icons. Enable this functionality
   ```bash copy
   sudo apt install libayatana-appindicator3-1 gir1.2-ayatanaappindicator3-0.1 gnome-shell-extension-appindicator
   ```
8. Clean up and remove old files
   ```bash copy
   cd ~/Downloads && rm -r protonvpn-stable-release_1.0.4_all.deb
   ```
9. Headover to [ProtonVPN](https://account.protonvpn.com/signup "ProtonVPN.com") and Sign-up to a free account.


**_Connect to ProtonVPN whenever accessing a web browser on your machine._**

---
# Install Mullvad VPN (optional) 
[Mullvad](https://mullvad.net/en/download/vpn/linux "Mullvad.net") recommended by the official Tor website. It's a paid service but has no email requirement and can use BTC to pay for the service. The internet speed should also be faster than a free ProtonVPN account.

___
# Install Brave Browser (optional)
1. Enter the following commands one at a time. Run:
   ```bash copy
   sudo apt install curl
   ```
2. Download keys to keychain
   ```bash copy
   sudo curl -fsSLo /usr/share/keyrings/brave-browser-archive-keyring.gpg https://brave-browser-apt-release.s3.brave.com/brave-browser-archive-keyring.gpg
   ```
3. Verify  
   ```bash copy
   echo "deb [signed-by=/usr/share/keyrings/brave-browser-archive-keyring.gpg] https://brave-browser-apt-release.s3.brave.com/ stable main"|sudo tee /etc/apt/sources.list.d/brave-browser-release.list
   ```
4. Update and install 
   ```bash copy
   sudo apt update && sudo apt install brave-browser
   ```

---
# Install Telegram Desktop (optional)
A quick solution for encrypted files/messages.
1. Install Telegram from apt repo. Run:
   ```bash copy
   sudo apt install telegram-desktop
   ```

---
# Install Bitcoin Knots
Head over to [Bitcoin Knots](https://bitcoinknots.org/) and:
- Download the latest Linux(tgz) 64 bit version and save to Downloads folder
- Bitcoin Knots is a derivative of Bitcoin Core with enhanced features, more conservative policies, and additional privacy options
- Follow the verification instructions on the Bitcoin Knots website to verify your download using GPG signatures

## Complete install
[Reference Link](https://bitcoin.org/en/full-node#linux-instructions "Bitcoin.org")

1. Unzip the bitcoin knots folder (adjust filename for current version)
   ```bash copy
   tar xzf bitcoin-28.1.knots20250305-x86_64-linux-gnu.tar.gz
   ```
2. Install bitcoin knots
   ```bash copy
   sudo install -m 0755 -o root -g root -t /usr/local/bin bitcoin-28.1.knots20250305/bin/*
   ```
3. Clean up (adjust filenames as needed)
   ```bash copy
   cd ~/Downloads && sudo rm -r bitcoin-28.1.knots20250305-x86_64-linux-gnu.tar.gz SHA256SUMS.asc SHA256SUMS
   ```

---
## Run Bitcoin Knots (start initial blockchain download)

1. Start Bitcoin Knots. Run:
   ```bash copy
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
   ```bash copy
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
   ```bash copy
   bitcoin-cli stop
   ```
## Allow incoming connections (optional but recommended)
Configure your WIFI router to allow Bitcoin Knots incoming connections on port:8332. Make a note of both your MAC and IP address then follow the instructions in this [Link](https://bitcoin.org/en/full-node#network-configuration)

Retrieve your Laptops MAC address and IP address from the Terminal. 

1. To print your MAC address to Terminal. Run:
   ```bash copy
   ip link
   ```
   You can find the MAC address of your device at the last line after ```link/ether=##:##:##:##:##:##```.

2. Print your IP address to Terminal
   ```bash copy
   hostname -I
   ```
## Some other helpful commands
3. Install net-tools to check incoming/outgoing port traffic
   ```bash copy
   sudo apt install net-tools
   ```
4. Check what IP and port Bitcoin is listening to
   ```bash copy
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
**Last updated: July 2025**
[Official website](https://support.torproject.org/apt/tor-deb-repo/)

"Browse Privately. Explore Freely.
Defend yourself against tracking and surveillance. Circumvent censorship." - Torproject.org

1. Verify your CPU architecture. Run:
   ```bash copy
   dpkg --print-architecture
   ```
2. Install apt-transport-https
   ```bash copy
   sudo apt install apt-transport-https
   ```
3. Check what Linux Distribution you have installed
   ```bash copy
   lsb_release -c
   ```
4. Create a new file in /etc/apt/sources.list.d/ named tor.list
   ```bash copy
   cd /etc/apt/sources.list.d/
   ```
5. Open the file
   ```bash copy
   sudo nano tor.list
   ```
6. Add the following entries inside the file, save and close
   ```bash copy
   deb     [arch=amd64 signed-by=/usr/share/keyrings/deb.torproject.org-keyring.gpg] https://deb.torproject.org/torproject.org noble main
   deb-src [arch=amd64 signed-by=/usr/share/keyrings/deb.torproject.org-keyring.gpg] https://deb.torproject.org/torproject.org noble main
   ```
7. Add Tor gpg key used to sign the packages
   ```bash copy
   sudo wget -qO- https://deb.torproject.org/torproject.org/A3C4F0F979CAA22CDBA8F512EE8CBC9E886DDD89.asc | gpg --dearmor | sudo tee /usr/share/keyrings/deb.torproject.org-keyring.gpg >/dev/null
   ```
8. Update apt
   ```bash copy
   sudo apt update
   ```
9. Install Tor
   ```bash copy
   sudo apt install tor deb.torproject.org-keyring
   ```
10. Check Tor is installed
    ```bash copy
    tor --version
    ```
11. Configure Tor to start at system Boot (optional but recommended)
    ```bash copy
    sudo systemctl enable tor
    ```

## Tor Systemctl commands
1. Manage Tor using systemd
   ```bash copy
   sudo systemctl restart tor
   ```
2. To check the status
   ```bash copy
   sudo systemctl status tor
   ```

---
## Set up Tor hidden service
Configure Bitcoin Knots to only connect using Tor. [Reference link](
https://en.bitcoin.it/wiki/Setting_up_a_Tor_hidden_service)

Additional video tutorial, for further reference: [Canadian Bitcoiners](
https://www.youtube.com/watch?v=goTkOt8Rr1Q&list=PLZqQw4mLW-r3UEyL12FG4koZq6lOLsURF&index=3)

1. Make changes to Tor configuration file. Run:
   ```bash copy
   cd /etc/tor
   ```
2. Open torrc file   
   ```bash copy
   sudo nano torrc
   ```
3. Enter the below text at the bottom of the file, save and exit
   ```bash copy
   ControlPort 9051
   CookieAuthentication 1
   CookieAuthFileGroupReadable 1
   ```
4. Check what your Bitcoin Knots user name is
   ```bash copy
   ps -eo user,group,comm |egrep 'bitcoind|bitcoin-qt' |awk '{print "Bitcoin user: " $1}'
   ```
5. Now add your Bitcoin Knots user name to your Tor group. For example my command would be ```sudo usermod -a -G debian-tor rez``` as my Bitcoin user name is rez.
   ```bash copy
   sudo usermod -a -G debian-tor <user name found from above command>
   ```
6. If the above command did not work, double check your Tor user group name, run this command for a list of user groups, look for a user group with Tor in it's name.
   ```bash copy
   getent group
   ```
   
The above configuration sets up an automatic hidden service that is initiated by Bitcoin Knots. On the next startup of bitcoin, Bitcoin Knots will generate a file called ```onion_private_key``` in the data directory. KEEP THIS SAFE. If someone copies this file they can run a server with your .onion address. While a malicious party cannot necessarily associate the server with you as a person, as long as your server has the same xxxx.onion address they will know it is run by the same person.

If you delete this file, the next time bitcoind loads it will generate a new key file and xxxxxxxx.onion address.  For absolute security delete your ```onion_private_key``` file at each reboot or some frequent interval.

7. Do a system Restart
   ```bash copy
   sudo shutdown -r now
   ```

## Verify Bitcoin Knots uses Tor. Option: 1
1. Start Bitcoin Knots GUI 
   ```bash copy
   bitcoin-qt
   ```
2. Once loaded enter the ```Network``` screen by pressing ```CTL+N```.
3. Click on the ```Peers``` tab.
   You should now see a list of all the Bitcoin peers that your node is connected too. Under the ```Network``` column all the row values should say ```Onion```, meaning you are only connected to    peers over the onion ntwork. 

## Verify Bitcoin Knots uses Tor. Option: 2
1. Check Bitcoin Knots ```NetworkInfo```. From the Bitcoin Knots GUI click 'Window' tab, 'Consol', then type the below command after the ```>``` and press enter.
   ```bash copy
   getnetworkinfo
   ```
2. Scroll up until you see the networks section. Your node is running behind Tor if the 'ipv4' and 'onion' networks have the below settings (there will also be other settings in each network group but they can be ignored):
   ```
   "name": "ipv4",
         "limited": true,
         "reachable": false

   And

   "name": "onion",
         "limited": false,
         "reachable": true
   ```

## Verify Bitcoin Knots uses Tor. Option: 3
You will learn a lot about what Bitcoin Knots is doing during start-up and shut-down if you watch the debug.log file.

1. Navigate to you main Bitcoin data-directory. 
   ```bash copy
   cd ~/.bitcoin
   ```
2. Ooen a new Terminal window, will will call this 'Terminal 1'. Activate tail on the Bitcoin Knots debug.log file with a grep on Tor.
   ```bash copy
   tail -f debug.log | grep tor
   ```
2. Now in a new Terminal window start bitcoind with debug set to Tor.
    ```bash copy
    bitcoind --daemon --debug=tor
    ```
3. Watch the debug file output printed in Terminal 1. You will see ```Tor: ADD_ONION successful``` and a lot of other Tor actions printed to the Terminal that Bitcoin Knots completed during start-up including starting a ```Tor control thread```, opening a ```Tor connection``` and finally connecting to the Tor network using your Tor encryption key.


---
# Install Electrs
[Official website](https://github.com/romanz/electrs/tree/master?tab=readme-ov-file)

"Electrs is a great low-resource, easy-to-install option for personal use - especially on resource-constrained hardware." - [Jameson Lopp](https://blog.casa.io/electrum-server-performance-report/)

## Build dependencies
1. Install recent Rust
   ```bash copy
   curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
   ```
2. Install Cargo
   ```bash copy
   sudo apt install cargo
   ```
3. Update package manager
   ```bash copy
   sudo apt update
   ```
4. Install dependencies for Rust-RocksDB
   ```bash copy
   sudo apt install clang cmake build-essential
   ```

I chose to compile electrs by statically linking to librocksdb, which has less dependencies.

5. Install dependencies 
   ```bash copy
   sudo apt install -y libgflags-dev libsnappy-dev zlib1g-dev libbz2-dev liblz4-dev libzstd-dev
   ```
6. Clone the repo
   ```bash copy
   git clone -b v7.8.3 --depth 1 https://github.com/facebook/rocksdb && cd rocksdb
   ```
7. Install using make
   ```bash copy
   make shared_lib -j $(nproc) && sudo make install-shared
   ```
8. Clean up directory
   ```bash copy
   cd .. && rm -r rocksdb
   ```
9. Prepare man page generation (optional)
   ```bash copy
   cargo install cfg_me
   ```
10. Move to home directory and download electrs repo
    ```bash copy
    cd ~ && git clone https://github.com/romanz/electrs
    ``` 
11. Move into electrs directory
    ```bash copy
    cd electrs
    ```
## Build Electrs
Note: you need to have enough free RAM to build electrs. The build will fail otherwise. Close those 100 old tabs in the browser. 

12. First build should take ~20 minutes
    ```bash copy 
    cargo build --locked --release
    ```
    During installation build the below warning was thrown:

    ```bash
    warning: electrs (lib) generated 1 warning (run cargo fix --lib -p electrs to apply 1 suggestion)
    Finished release [optimized] target(s) in 5m 53s
    ```

    I ran the command, suggested in the above warning, which completed the build without further errors.
    ```bash copy
    cargo fix --lib -p electrs
    ```

## Generate Electrs man pages (optional)
Run ```cfg_me man``` to see man page immediately or run ```cfg_me -o electrs.1 man``` to save it into a file (```electrs.1```).


---
## Configure Electrs
1. First lets create a symbolic link to a directory that is in our PATH so we can run electrs from anywhere  
   ```bash copy
   sudo ln -s /home/<USER>/electrs/target/release/electrs /usr/local/bin/electrs
   ```
2. Check symbolic link was created
   ```bash copy
   ls -l /usr/local/bin
   ```
   Now when we upgrade to a new release we won't need to do this again as the link should still work.

3. Test the link
   ```bash copy
   electrs --version
   ```
   If the terminal displays a version number then the link is working and we can now run Electrs simply by running ```electrs``` from any location.   
     
4. Create a config file for Electrs
   ```bash copy
   cd ~ && sudo mkdir .electrs && sudo nano .electrs/config.toml   
   ```
5. Copy below text into config.toml, save and exit
   ```bash copy
   # DO NOT EDIT THIS FILE DIRECTLY - COPY IT FIRST!
   # If you edit this, you will cry a lot during update and will not want to live anymore!
   
   # This is an EXAMPLE of how configuration file should look like.
   # Do NOT blindly copy this and expect it to work for you!
   # If you don't know what you're doing consider using automated setup or ask an experienced friend.
   
   # This example contains only the most important settings.
   # See docs or electrs man page for advanced settings.
   
   # File where bitcoind stores the cookie, usually file .cookie in its datadir
   #cookie_file = "/media/<USER>/<External_SSD_Name>/.cookie"

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
6. Check size of current Bitcoin Knots block directory
   ```bash copy
   du -ch ~/.bitcoin/blocks/blk*.dat | tail -n1
   ```
   This will print the size of the existing Bitcoin Knots block directory. The final Electrs index DB will be about 10-20% the size of the Bitcoin Knots block directory.

7. Start Bitcoind and wait for bitcoind to complete initial sync.
   ```bash copy
   bitcoind -server -daemon
   ```

8. Check sync is complete (the "blocks" & "headers" number needs to match, if not then there are still blocks being downloaded and synced).
   ```bash copy
   bitcoin-cli getblockchaininfo | head
   ```
   
9. Start Electrs initial sync. First sync can take 1-2 days depending on CPU/hardware.
   ```bash copy
   electrs --log-filters INFO
   ```
10. Check final size of Electrs server index DB (should be around 10% the size of the Bitcoin Knots block directory we checked earlier).
   ```bash copy
   du ~/electrs/db
   ```
## Monitoring Electrs (optional)
1. Install prometheus
   ```bash copy
   sudo apt install prometheus
   ```
3. Edit prometheus.yml file
   ```bash copy
   cd /etc/prometheus/ && sudo nano prometheus.yml
   ```
   Scroll to the bottom of the file and add the below, save and exit.
     ```bash copy
      - job_name: electrs
        static_configs:
          - targets: ['localhost:4224']
      ```
4. Restart prometheus
     ```bash copy
     sudo systemctl restart prometheus
     ```
6. Check collected metrics
     ```bash copy
      brave-browser 'http://localhost:9090/graph?g0.range_input=1h&g0.expr=index_height&g0.tab=0'
      ```
Click on ```Status``` tab then ```Runtime & Build Information``` tab to see if prometheus loaded and is pulling stats for further user querying.  
  
---
# Install Electrum
[Official website](https://electrum.org/#download)

Electrum was first released as open-source back in 2011, making it one of the most trusted Bitcoin wallets available.
1. Download ThomasV public key and import into keychain. Run:
   ```bash copy
   cd ~/Downloads && wget https://raw.githubusercontent.com/spesmilo/electrum/master/pubkeys/ThomasV.asc && gpg --import ThomasV.asc
   ```
2. Install dependencies. Run:
   ```bash copy
   sudo apt-get install python3-pyqt5 libsecp256k1-dev python3-cryptography
   ```
3. Download package
   ```bash copy
   wget https://download.electrum.org/4.5.8/Electrum-4.5.8.tar.gz
   ```
4. Verify signatures
   ```bash copy
   wget https://download.electrum.org/4.5.8/Electrum-4.5.8.tar.gz.asc && gpg --verify Electrum-4.5.8.tar.gz.asc
   ```
5. Install with pip
   ```bash copy
   sudo apt-get install python3-setuptools python3-pip && python3 -m pip install --user Electrum-4.5.8.tar.gz
   ```
6. Clean up
   ```bash copy
   cd ~/Downloads && sudo rm -r Electrum-4.5.8.tar.gz Electrum-4.5.8.tar.gz.asc ThomasV.asc
   ```


---
## Configure Electrum
The Electrum config file is located in a hidden Electrum directory, however this directory is only created once Electrum is run for the first time. To prevent any privacy leaks we can run Electrum with some flags to make sure it only connects to our Electrs server.
1. Launch Electrum using the following flags
   ```bash copy
   electrum --oneserver --server 127.0.0.1:50001:t --proxy socks5:127.0.0.1:9150
   ```
   Once Electrum loads, immediatly close it down again so we can edit the config file that was just created.
 
2. Open Electrum config file
   ```bash copy
   cd ~/.electrum && nano config
   ```
6. Replace the contents of the file with the below. save and exit:
   ```bash copy
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
   This is what each config setting does:
      - auto_connect: false = Don't auto connect to read headers at startup
      - check_updates: false = Dont check for updates
      - decimal_point: 8 = Use BTC not sats
      - log_to_file: true = Log debugging to logs/ folder in data directory 
      - oneserver: true = Only connect to one server
      - proxy: socks4:localhost:9050 = Use tor proxy
      - proxy_password: "" = No password for tor proxy
      - proxy_user: "" = No user deets for tor proxy
      - server: localhost:50001:t = Connect to electrs without ssl

The next time we start Electrum we can simply run the command ```electrum``` and let the config file handle the rest.

## Create a Test wallet
We will create a new test (hot) wallet in Electrum to confirm and verify our config settings are correct.
1. Start electrum. Run:
   ```bash copy
   electrum
   ```
2. At the welcome screen. Click ```Next```.
3. Rename ```default_wallet``` to ```test_hot_wallet``` (I think this name is less confusing). Click ```Next```.                                                                        
4. Select ```I already have a seed```. Click ```Next```.
5. Head over to [CoinPlate](https://getcoinplate.com/bip39-seed-phrase-mnemonics-generator-offline-online-tool/?v=2a6039655313 "CoinPlate's Homepage") and generate a Bip39 24 word seed phrase .
   Copy and save the seed phrase to a note on your desktop. Don't worry about security as this is just a simple test wallet for testing configuration settings.
6. Copy and paste the seed phase into the Electrum box that is displayed.
7. Click ```Options```, and select ```Bip39 seed```. Click ```OK```. Ignore the warning and click ```Next```.
8. Keep ```native segwit (p2wpkh)``` selected and click ```Next```.
9. Leave the password fields blank, we wont encrypt the wallet data as this is just a test wallet, click ```Next```.
10. Electrum - enable update check. Click ```No```. We will always verify and update our software ourselves.

## Add some watch-only addresses
We will use these to confirm Electrs & Bitcoin Knots are connected correctly.
1. From the Electrum window press CTRL+N, this will bring up the ```New/Restore``` menu.
2. Choose a name for your wallet, you can just name the wallet something like ```satoshi_address``` or ```mr100```. Click ```Next```.
3. Select ```Import Bitcoin addresses or private keys```, click ```Next```.
4. Add any bitcoin addresses that you would like to watch. A simple Google search can return some interesting famous bitcoin addresses. I find it more intuative to create a new watch wallet for each address. Out of curiosty and fun, I added the following three addresses to three individual wallets named ```satoshi_address, huobi_address and mr100_address```. Just add the actual address (long string of 34 characters). i.e if you want to watch mr100 bitcoin address just add ```1Ay8vMC7R1UbyCCZRVULMV7iQpHSAbguJP``` and click ```Next```.

   - 1A1zP1eP5QGefi2DMPTfTL5SLmv7DivfNa (satoshi_address, shows first Bitcoin transaction to Hal Finney) 
   - 35hK24tcLEWcgNA4JxpvbkNkoAcDGqQPsP (Huobi_address = Huobi exchange hot wallet)
   - 1Ay8vMC7R1UbyCCZRVULMV7iQpHSAbguJP (mr100_address = Unknown, transacts daily in blocks of 100 BTC)
   
6. No need to set a wallet password as your just watching someone elses Bitcoin address. Click ```Finish```.

Footnote: Although it's great to watch something smash buy bitcoin in blocks of 100 at the same time there is always an equal seller for instance the legendary Gummo telling the world in 2024 that he's selling 72,572 bitocoin in blocks of 100🤔

[X post](https://x.com/pete_rizzo_/status/1837477503520149913?t=CVB1uNKjNts1G2JASxUpXA&s=19) - The Bitcoin Historian @pete_rizzo_

_"I'm taking steps to sell the remaining 72,572 bitcoins responsibly! 💼 No deals with organised crime, third parties, or middlemen - just direct transactions with integrity. Selling in lots of 100 for transparency only. Let's keep it real & legal in the crypto world!💰" - Gummo_

---
# Launch Bitcoin Knots, Electrs & Electrum
1. Start Bitcoin Knots by running ```bitcoin-qt``` to use the GUI or to run a daemon. Run:
   ```bash copy
   bitcoind -datadir=/media/<User>\<External_SSD_Name> -server -daemon
   ```
2. Start Electrs once Bitcoin Knots has fully loaded
   ```bash copy
   electrs --log-filters INFO --network bitcoin --db-dir ~/electrs/db --daemon-dir /media/<User>\<External_SSD_Name>
   ```
5. Start Electrum once Electrs has fully indexed and is at te blockchain tip. You can check this by looking at the Terminal printout and waiting for the ```INFO electrs::chain chain updated```. Electrum will not sync until Electrs has synced to the tip of the Blockchain. So wait for the ```INFO electrs::chain chain updated``` and you are good to launch Electrum.
   ```bash copy
   electrum
   ```
If the ```Network``` light in the bottom righthand corner of Electrum GUI is blue then you are connected to your own node (which we configured & verified is running behind Tor). It is now safe to interact with your real wallets.

---
# Install Specter wallet
[Official Website](https://specter.solutions/index.html)

Specter is an open-source Bitcoin wallet, first released June 2020. It offers an intuative desktop GUI ideal for the creation and management of MultiSig or SingleSig wallets with extensive HWW support.

## Install Python 3.10 for Specter Compatibility

Bitcoin Knots 28.1 requires a newer version of Specter than the current binary releases support. We'll install Specter via Python virtual environment for the latest compatible version.

- Add deadsnakes PPA for Python 3.10. Run:
```bash copy
sudo apt install software-properties-common
sudo add-apt-repository ppa:deadsnakes/ppa
sudo apt update
sudo apt install python3.10 python3.10-venv python3.10-dev python3-venv
```

- Create Python virtual environment with Python 3.10. Run:
```bash copy
python3.10 -m venv ~/.specter-env
source ~/.specter-env/bin/activate
```

- Install Specter Browser App. Run:
```bash copy
pip install --upgrade pip
pip install cryptoadvance.specter
```

- Remove problematic Spectrum plugin (causes SQLAlchemy conflicts). Run:
```bash copy
pip uninstall cryptoadvance-spectrum -y
```

- Check installed version. Run:
```bash copy
pip show cryptoadvance.specter
```

- Create launch script for easy startup. Run:
```bash copy
nano ~/start-specter-desktop.sh
```

- Add the following content to the script, save and exit:
```bash copy
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

# Wait for server to start (check every second for up to 10 seconds)
echo "Waiting for Specter to start..."
for i in {1..10}; do
    if check_specter; then
        echo "Specter started successfully!"
        sleep 2  # Give it a moment to fully initialize
        brave-browser http://127.0.0.1:25442
        exit 0
    fi
    sleep 1
done

echo "Failed to start Specter server. Check ~/.specter/specter.log for errors."
exit 1
```

- Make the script executable. Run:
```bash copy
chmod +x ~/start-specter-desktop.sh
```

- Download an application icon for Specter:
I think the red Pacman logo looks good for Spector.

Head over to [FreeiconsPNG](https://www.freeiconspng.com/download/25184) and download the Pacman PNG logo to your Downloads folder.

- Move Pacman logo to icons folder. Run:
```bash copy
mv ~/Downloads/pacman-png-25184.png ~/.icons/specter-logo.png
```
Adjust the filename to match what you actually downloaded

```bash copy

# Move your pacman logo to the icons folder
mv ~/Downloads/pacman-png-25184 ~/.icons/specter-logo.png
# Or copy if you want to keep the original
cp ~/path/to/your/pacman.png ~/.icons/specter-logo.png
```

- Create desktop launcher. Run:
```bash copy
nano ~/Desktop/specter.desktop
```

- Add the following content, save and exit:
```bash copy
[Desktop Entry]
Version=1.0
Type=Application
Terminal=true
Icon=/home/rez/.icons/specter-logo.png
Name=Specter Desktop
Exec=/home/<USER>/start-specter-desktop.sh
Comment=Bitcoin wallet with hardware wallet support
```
Replace <USER> with your actual username.

- Make desktop launcher executable. Run:
```bash copy
chmod +x ~/Desktop/specter.desktop
```

-  Make sure files have correct permissions. Run:
```bash copy
chmod 644 ~/.icons/specter-logo.png
chmod +x ~/Desktop/specter.desktop
```

## Set UDEV Rules for Hardware Wallets

Hardware wallets require specific UDEV rules to function properly with Linux systems.

- Create plugdev group and add your user. Run:
```bash copy
sudo groupadd plugdev
sudo usermod -aG plugdev `whoami`
```

- Download UDEV rules for popular hardware wallets. Run:
```bash copy
# Create temporary directory for UDEV rules
mkdir -p ~/temp-udev && cd ~/temp-udev

# Download Specter's comprehensive UDEV rules collection
wget https://raw.githubusercontent.com/cryptoadvance/specter-desktop/master/udev/51-coinkite.rules
wget https://raw.githubusercontent.com/cryptoadvance/specter-desktop/master/udev/51-hid-digitalbitbox.rules
wget https://raw.githubusercontent.com/cryptoadvance/specter-desktop/master/udev/51-usb-keepkey.rules
wget https://raw.githubusercontent.com/cryptoadvance/specter-desktop/master/udev/51-usb-ledger.rules
wget https://raw.githubusercontent.com/cryptoadvance/specter-desktop/master/udev/51-usb-trezor.rules
```

- Install UDEV rules. Run:
```bash copy
sudo cp *.rules /etc/udev/rules.d/
sudo udevadm trigger
sudo udevadm control --reload-rules
```

- Clean up temporary files. Run:
```bash copy
cd ~ && rm -rf ~/temp-udev
```
  
## Specter configuration
- Start Bitcoin Knots by running `bitcoin-qt` or `bitcoind -daemon`
- Start Specter by double-clicking the desktop icon or running `./start-specter-desktop.sh` (this will automatically open your browser)
You will be greeted with Specters welcome screen providing the options to configure the application. 

8. Use the below config settings:
   - Name = Bitcoin Knots
   - Username = <UserName> (matching the rpcuser details in bitocoin.conf file)
   - Password = <Password> (matching the rpcpassword details in bitcoin.conf file)
   - Host = 127.0.0.1
   - Port = 8332
   
9. Click ```Connect```

Specter will automatically utilize the existing Tor configuration used for Bitcoin Knots. To validate this yourself, you can check the Specter Desktop logs for any Tor-related messages or errors. If everything is configured correctly, you should see no issues or warnings regarding Tor.

10. Check Specter logs for any errors/issues
    ```bash copy
    cd ~/.specter && nano specterApp.log
    ```   
11. Clean up, delete old files/directories
    ```bash copy
    cd ~/Downloads && rm -r Specter   
    ```
Read Specters official [docs](https://docs.specter.solutions/desktop/) to get the most out of the software wallets functionality.

---
# Troubleshooting

## Specter Connection Issues

If you encounter `KeyError: 'error'` when connecting Specter to Bitcoin Knots 28.0:

1. **Ensure you're using the Python installation method**: Binary releases may not support Bitcoin Knots 28.0
2. **Check Bitcoin Knots is running**: Run `bitcoin-cli getblockchaininfo` to verify
3. **Verify RPC credentials**: Ensure rpcuser and rpcpassword in bitcoin.conf match Specter settings
4. **Check Specter version**: Run `pip show cryptoadvance.specter` - should be v2.1.1 or later

## Port Conflicts

If you get "Port 25442 is in use":
- Kill existing Specter processes: `pkill -f "cryptoadvance.specter"`
- Or use a different port: `python -m cryptoadvance.specter server --host 127.0.0.1 --port 25443`

## SQLAlchemy Conflicts

If you see SQLAlchemy errors during Specter installation:
- Remove the Spectrum plugin: `pip uninstall cryptoadvance-spectrum -y`
- Reinstall Specter: `pip install --force-reinstall cryptoadvance.specter`

## Hardware Wallet Issues

If hardware wallets aren't detected:
- Ensure UDEV rules are installed correctly
- Check that your user is in the plugdev group: `groups $USER`
- Try unplugging and reconnecting the device
- Restart Specter after connecting hardware wallet
  
---
# Install Sparrow wallet
[Official Website](https://sparrowwallet.com/)

Sparrow is an open-source Bitcoin wallet, first released September 2020, offering exellent wallet encryption, keeping the wallet open for as limited time as possible for added security. The encrypted wallet file can also be saved to a seperate location (external flash drive etc.) for additional plausible deniability. 

1. Verify your CPU architecture. Run:
   ```bash copy
   dpkg --print-architecture
   ```
2. Head over to [Sparrow Downloads](https://sparrowwallet.com/download/) and download:
   - sparrow_2.2.3-1_amd64.deb (for Ubuntu 24.04)
   - sparrow-2.2.3-manifest.txt
   - sparrow-2.2.3-manifest.txt.asc
   
   Save all files to your Downloads folder.
   
3. Scroll the Sparrow/Downloads page and follow the instruction under the heading ```Verifying the release``` to verify your download. It doesnt make sense to install software then use that software to verify itself so we will verify manually using gpg. Scroll down the official Sparrow download page further for the manual vefification instructions using gpg.
4. Download and import craigraw/pgp_keys.asc
   ```bash copy
   curl https://keybase.io/craigraw/pgp_keys.asc | gpg --import
   ```
5. Verify the signature of the manifest file
   ```bash copy
   cd ~/Downloads && gpg --verify sparrow-2.2.3-manifest.txt.asc
   ```
6. Verify the download file
   ```bash copy
    sha256sum --check sparrow-2.2.3-manifest.txt --ignore-missing
   ```
   If you recieve the ```OK``` result to your terminal then the solftware is authentic and safe to install. This also means that we can now use Sparrows veification feature to easily verify future software from the GUI interface if we wish.
   
## Install and configure  
7. Navigate to Downloads folder and install the downloaded .deb file. This will save the app to your ```Show Applications``` folder, that can be accessed from your Desktop.
   ```bash copy
   cd ~/Downloads && sudo dpkg -i sparrow_2.2.3-1_amd64.deb  
   ```
8. Start Sparrow by double clicking the app icon.
9. Read the welcome messages and then choose ```Server: type```, ```Private Electrum``` (the blue toggle switch).
10. Enter these config settings
   - URL: 127.0.0.1 50001
   - Use SSL: toggle switch ```Off```
   - Certificate: (leave the field empty)
   - Use Proxy: toggle switch ```On``` (blue)
   - Proxy URL: 127.0.0.1 9050
11. Make sure Bitcoin Knots and Electrs are running then click on the    
```Test Connection``` button. You should be greeted with the following text:
    ```
    Connected to electrs/0.10.x on protocol version 1.4
    Batched RPC enabled.
    Server Banner: Welcome to electrs 0.10.x (Electrum Rust Server)!
    ```
12. Clean up, delete old files/directories
    ```bash copy
     cd ~/Downloads && rm -r sparrow_2.2.3-1_amd64.deb sparrow-2.2.3-manifest.txt.asc sparrow-2.2.3-manifest.txt
    ```
### Important: Linux Package Rename
**Note for Linux users:** The Sparrow package has been renamed from `sparrow` to `sparrowwallet` starting with version 2.2.0. If you have an older version installed, you may need to:

13. Remove the old package:
    ```bash
    sudo apt remove sparrow
    # Check if old files exist and remove manually:
    sudo rm -rf /opt/sparrow
    ```
14. Verify the new installation is in the correct location. Run:
    ```bash copy
    ls /opt/sparrowwallet
    ```
       
Read Sparrows official [docs](https://sparrowwallet.com/docs/) to get the most out of the software wallets functionality. 

---
# Hardware Wallet support
Linux systems require udev rules from each Hardware device manufacturer to allow the USB functionality to work. These were all included during the installation of Specter (as Specter privided a handy folder containing all the most popular hardware device Udev rules for Linux).

## Electrum HWW support
[Reference Link](https://electrum.readthedocs.io/en/latest/hardware-linux.html)
1. For electrum we just need to downgrade pip to allow installation of required dependencies for Electrum HWW support. Run:
   ```bash copy
   python3 -m pip uninstall pip && python3 -m pip install pip==22
   ```
2. Install dependencies
   ```bash copy
   python3 -m pip install hidapi btchip-python ecdsa ledger-bitcoin
   ```
3. Upgrade pip back to latest version
   ```bash copy
   sudo pip3 install --upgrade pip
   ```
   
## Install Ledger Live (optional)
[Reference Link](https://support.ledger.com/article/4404389606417-zd)

If you are still using Ledger or needing access to to the Ledger Live suite then follow below instructions to install.

1. Add udev rules for Ledger (if not already done so) to allow USB access to your Ledger device
   ```
   wget -q -O - https://raw.githubusercontent.com/LedgerHQ/udev-rules/master/add_udev_rules.sh | sudo bash
   ```
2. Install Ubuntu 24.04 LTS dependency
   ```bash copy
   sudo add-apt-repository universe
   ```
3. Head over to [Official website](https://download.live.ledger.com/latest/linux) and download the Linux .Appimage file to your Downloads folder.
4. Shorten the name and move to the ```home``` directory
   ```bash copy
   mv ledger-live-desktop-2.91.1-linux-x86_64.AppImage ~/LedgerLive-2.91.1.AppImage
   ```
5. Run Ledger-Live for the first time (after the first run the app will be added to your ```Show Applications``` folder via the desktop Toolbar.
   ```bash copy
   cd ~ && ./LedgerLive-2.91.1.AppImage
   ```
   
---
# Configure desktop
## Build Bitcoin node desktop icon
Build a launchable Desktop icon called ```Bitcoin``` that when clicked will launch Bitcoin Knots and Electrs, ready for you to then open the bitcoin wallet of your choice.
1. First we need to create an executable bash script, we'll call it ```node.sh```
   ```bash copy
   nano node.sh
   ```
2. Edit the file with your application launch paths
   ```bash copy
   #!/bin/bash
   
   # launch bitcoin-qt as a background job
   #/usr/local/bin/bitcoin-qt &
   
   # launch bitcoind as a background job
   /usr/local/bin/bitcoind &
   
   # Sleep to allow Bitcoin Knots to load, if electrs throws an error then increase the sleep time
   sleep 5
   
   # launch electrs
   /usr/local/bin/electrs --log-filters INFO
   
   exit 0

   ```

3. Make the file executable
   ```bash copy
   chmod +x node.sh
   ```
4. Check if you have a .icon directory
   ```bash copy
   cd ~/.icon
   ```
   If you get the error ```No such file or directory```. Then create the directory.
   ```bash copy
      mkdir ~/.icons
   ```  
4. Move to ```~/.icons``` directory and download a Bitcoin logo icon
   ```bash copy
   cd ~/.icons && wget https://bitcoin.design/assets/images/guide/getting-started/visual-language/bitcoin-symbol.svg
   ```
5. Shorten the file name and move the file to the icon directory
   ```bash copy
   mv bitcoin-symbol.svg btclogo.svg
   ```
6. Create a new file named bash.desktop in the home directory (same location as your node.sh file). This file will contain the desktop entry information.
   ```bash copy
   cd ~ && nano bitcoin.desktop
   ```
7. Edit the file adding the following information, save and exit:
   ```bash copy
   [Desktop Entry]
   Version=1.0
   Type=Application
   Terminal=true
   Icon=btclogo
   Name=Bitcoin
   Exec=/home/<user>/node.sh
   Comment=Run Bash Script
   ```

8. Validate the bash.desktop file using the desktop-file-validate command
   ```bash copy
   desktop-file-validate bitcoin.desktop
   ```
   If there are no errors, the file is valid.

9. Move the bash.desktop file to Desktop
   ```bash copy
   mv bitcoin.desktop ~/Desktop
   ```

   Log out and log back in to your system to ensure the icon is updated.

10. Right-click the desktop icon, select ```Allow Launching``` (or similar). The icon should now be visible and launchable.

11. Double click the desktop (Bitcoin) icon to Launch Bitcoin-qt and electrs together, or use the Terminal command:
    ```bash copy
    ./node.sh
    ```
## Build Electrum desktop icon
Build a launchable Desktop icon called ```Electrum``` that when clicked will launch the Electrum wallet.
1. Create a new .desktop file
  ``` bash copy
  touch ~/Desktop/electrum.desktop
  ```

2. Edit the new .desktop file
  ```bash copy
  nano ~/Desktop/electrum.desktop
  ```
3. Add the following into the file, save and close.
   ```bash copy
   [Desktop Entry]
   Name=Electrum
   Comment=Lightweight Bitcoin Wallet.
   GenericName=Bitcoin Wallet.
   Exec=/home/<USER>/.local/bin/electrum
   Icon=electrum
   Type=Application
   ```
4. Udate the shortcut’s permissions:
   ```bash copy
   chmod +x ~/Desktop/electrum.desktop
   ```
5. Also add a shortcut to your app-menu
   ```bash copy
   sudo cp ~/Desktop/electrum.desktop /usr/share/applications/
   ```
6. Right-click the desktop icon, select ```Allow Launching``` (or similar). The icon should now be visible and launchable.

7. Double click the desktop (Electrum) icon to Launch Electrum.  

## Remove HOME folder desktop icon
1. Remove Home folder icon
  ``` bash copy
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
- **Quick Setup Review ($150/hour)** - Troubleshooting and configuration fixes
- **Full Node Implementation ($300/session)** - Complete guided setup
- **Advanced Configuration ($450/session)** - Lightning Network and advanced features

**Benefits:**
- 1-on-1 expert guidance
- Non-technical user friendly
- Privacy-focused (no personal details required)
- Bitcoin payments accepted
- 30-day follow-up support

**Book Consultation:** [sovereign101.com/consultation](https://sovereign101.com/consultation)

*This consultation service helps support the continued development and maintenance of this free guide.*

---
