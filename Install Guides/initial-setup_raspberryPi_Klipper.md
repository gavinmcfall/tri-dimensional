# Install Setup of Raspberry Pi

1. Use Raspberry Pi imager to build an image
	1. Raspberry Pi OS Lite
	1. Set the:
		1. Hostname
		1. Admin Credentials
		1. SSH keys
1. Insert SD Into Raspberry Pi
1. sudo apt update && sudo apt upgrade
1. sudo reboot
1. login
1. nmtui
1. Set a fixed IP, gateway and dns servers
1. sudo reboot
1. login
1. sudo apt-get update && sudo apt-get install git -y
1. cd ~ && git clone https://github.com/dw-0/kiauh.git
1. ./kiauh/kiauh.sh
1. Install klipper, moonraker, and mainsail
1. cd /klipper
1. make menuconfig
1. For options, reference: https://github.com/bigtreetech/BIGTREETECH-SKR-mini-E3/blob/master/firmware/V3.0/Klipper/README.md
1. once configures, quit and save
1. make
1. Once complete, connect to the Pi using WinSCP and copy /klipper/out/klipper.bin to a local director on your PC