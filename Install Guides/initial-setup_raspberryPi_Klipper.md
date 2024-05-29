<!--
Markdown reference: https://www.markdownguide.org/basic-syntax/#ordered-lists
-->

# Install Setup of Raspberry Pi

1. Use Raspberry Pi imager to build an image
	1. OS: Raspberry Pi OS Lite
	1. Set the:
		1. Hostname
		1. Admin Credentials
		1. SSH keys
1. Insert SD Into Raspberry Pi
1. Run `sudo apt update && sudo apt upgrade`
1. Run `sudo reboot`
1. After the reboot, SSH back in
1. Run `nmtui` to configure Fixed IP
1. Configure
    1. fixed IP
    1. Gateway
    1. DNS Servers
1. Run `sudo reboot`
1. After the reboot, SSH back in
1. Run `sudo apt-get update && sudo apt-get install git -y`
1. Run `cd ~ && git clone https://github.com/dw-0/kiauh.git`
1. Run `./kiauh/kiauh.sh`
1. Install the following:
    1. Klipper
    1. Moonraker
    1. Mainsail
1. Note, you needs to be attentive so that the SSh session doesnt break as the install requires interaction
1. Run `cd /klipper`
1. Run `make menuconfig`
1. For options, reference: https://github.com/bigtreetech/BIGTREETECH-SKR-mini-E3/blob/master/firmware/V3.0/Klipper/README.md
1. Once configured, quit and save
1. Run `make`
1. Once complete, connect to the Pi using WinSCP and copy `/klipper/out/klipper.bin` to a local director on your PC