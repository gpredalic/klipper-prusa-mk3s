# Kliper on Prusa MK3s
Structured Klipper config for Prusa MK3s/MK3s+ 3D printer, inspired by https://github.com/Rat-OS/RatOS-configuration

Based on [dz0ny's MK3s Klipper config](https://github.com/dz0ny/klipper-prusa-mk3s) and [Ishan Jaidka's MK3s Klipper config](https://github.com/Ishan-Jaidka/Klipper-Cfg-Backup-Prusa-SKR1.4t-2209)

- Stock Prusa MK3s X, Y, E Motors
- Stock Prusa MK3s Frame
- Stock Prusa MK3s PSU 240W Delta
- Gates Belt
- BTT SKR 1.4 Turbo or NA
- TMC 2209
- 50W, 60W Heater Cartridge
- Dragon Hoten v2 HF Ceramic Core, Titanium, Copper Heat Sink 
- Termistor NTC100K or P10000 Pro
- 0.4 or 0.6 Nozzle (HS, CHT)
- Nylock Mod (M3x16mm, Nylon Washer, Nylon Nut)

## Pre-Check
- Get Z offset value from your current firmware (Menu -> Calibration -> Z-offset), you will need it for the Klipper config.
- Your bed needs to be perpendicular (based on XYZ Calibration). If not you will have to do the skew calibration before printing or you risk crashing your nozzle to the bed.
- Read https://github.com/gpredalic/klipper-prusa-mk3s/blob/main/printer.cfg.example
- Read https://www.klipper3d.org/Installation.html#building-and-flashing-the-micro-controller

## Install
1. Install https://docs.mainsail.xyz/setup/mainsail-os to SDCard and RPI
2. Connect as described in https://help.prusa3d.com/en/article/raspberry-pi-zero-w-preparation-and-installation_2180
3. Update all components under Machine tab, otherwise config might not be able to load
4. Clone config ```git clone https://github.com/gpredalic/klipper-prusa-mk3s.git ~/printer_data/config/klipper-prusa-mk3s```

  > If you are adding this configuration after installing Klipper via [KIAUH](https://github.com/th33xitus/kiauh), the directory might be different - typically following `~/[printer_name]/printer_data/config`, where `[printer_name]` is the name you selected during the Kiauh installation

5. Add the following to the to `moonraker.conf` to enable automatic updates

```yml
[update_manager PrusaMK3s]
type: git_repo
origin: https://github.com/gpredalic/klipper-prusa-mk3s.git
path: ~/printer_data/config/klipper-prusa-mk3s
primary_branch: main
is_system_service: False
managed_services: klipper
```

6. Copy or link https://github.com/gpredalic/klipper-prusa-mk3s/blob/main/printer.cfg.example to `printer.cfg` in your klipper config

To use this config, the firmware should be compiled for the LPC176X. To use via serial, in "make menuconfig" select "Enable extra low-level configuration options" and select **serial1** (the RasPi serial) or **serial0** when you plan to connect via the USB.

```
sudo apt update
sudo apt install python3 python3-venv python3-dev python3-pip git
cd ~/klipper
make menuconfig
make
cp ~/klipper/out/klipper.bin ~/klipper/out/firmware.bin
```
Copy the firmware.bin to the root of the USB flash drive, formated with FAT32 or exFAT 

## Nice things
[Klipper mesh on print area only install guide](https://gist.github.com/ChipCE/95fdbd3c2f3a064397f9610f915f7d02)

## Screenshots
![image](https://user-images.githubusercontent.com/239513/141822711-2818978e-2b87-4110-9b93-e5f489c9cdc7.png)
![image](https://user-images.githubusercontent.com/239513/141831204-89ced257-e67f-4b1f-add7-a3806cdd2617.png)
![image](https://user-images.githubusercontent.com/239513/141831245-11476041-240d-424a-8ff8-ffd8a03c08be.png)
![image](https://user-images.githubusercontent.com/239513/141831272-31b88652-ab3f-4978-8a4c-c54a83817dd1.png)
