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
1. Rename the `klipper.bin` to `firmware.bin` and copy onto a SD/MicroSD
1. Ensure the Printer is off
1. Insert the SSD/MircoSD into the printers motherboard and power on
1. Wait 5 minutes
1. Turn off the printer and remove teh SD/MicroSD
1. Turn the Printer back on
1. Connect the PI to the printer using a USB Cable
1. SSH into the Pi and run the following: `ls /dev/serial/by-id/*`
1. you should see sommething like: 
    ```ls /dev/serial/by-id/*
    /dev/serial/by-id/usb-Klipper_stm32f103xe_33FFD5055641343404761743-if00```
1. Next navigate to the IP address of the PI (the one you setup when you gave it a fixed IT) and you should see mainsail (The Klipper web interface)
    ![mailsail web interface image](images/mainsail_01.png)

1. click on `printer.cfg`
1. In the editor that shows up. Clear out everything
1. Then copy the entirety of this file and paste it into the `printer.cfg`:
    1. https://github.com/Klipper3d/klipper/blob/master/config/generic-bigtreetech-skr-mini-e3-v2.0.cfg
1. Next confirm where your CRTouch is connected to the motherboard. It should be here:
    ![motherboard pinout](images/btt_skr_mini_e3_v2.0_pinout_crtouch-location.png)
1. If it is then move on
1. add some more data to the `printer.cfg`
1. Undser `[stepper_z]` add the following line:
    1. `endstop_pin: probe:z_virtual_endstop`
1. Remove the following line:
    1. position_endstop: 0.0
1. Add the following to the bottom of the file:
    ```
    [bltouch]
    sensor_pin: ^PC13
    control_pin: PA1
    x_offset: 48.0
    y_offset: -2.0
    z_offset: 2.92
    pin_move_time: 0.4
    speed: 20

    [bed_mesh]
    speed: 120
    horizontal_move_z: 5
    mesh_min: 35, 6
    mesh_max: 240,198
    probe_count: 3,3
    algorithm: bicubic


    [homing_override]
    gcode:
        G1 Z10 F1200 
        G28 X Y
        G1 X115 Y115 F3000
        G28 Z
    set_position_z: 0.0
1. Next click `Save a restart`
1. Assuming you configured everything correctly you should see no errors and instead see a section that looks like this:
    ![mailsail web interface image](images/mainsail_02.png)
1. Next click on `Dashboard` in the left menu and under Toolhead Click: :house: All
1. The toolhead should move to approx center