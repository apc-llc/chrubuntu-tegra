##Install APC-branded Chrubuntu on Acer Chromebook CB5-311 for on-site CUDA trainings

Based on work of arm000 found [here](http://www.reddit.com/r/chrubuntu/comments/2hhb31/chrubuntu_on_acer_chromebook_13/)

### Instructions

1. Turn chromebook into developer mode:

```
sudo chromeos-firmwareupdate --mode=todev
```

2. Switch to developer terminal by pressing "Alt + Left Arrow", login as `chronos`

3. Download and execute the Chrubuntu installation script

```
wget https://goo.gl/i6ZjBV -O chrubuntu-tegra.sh
sudo bash ./chrubuntu-tegra.sh default lts
```

4. Redownload and re-run Chrubuntu instllation script after reboot

```
wget https://goo.gl/i6ZjBV -O chrubuntu-tegra.sh
sudo bash ./chrubuntu-tegra.sh default lts
```

5. After successfully entering Chrubuntu, reboot into ChromeOS and set Chrubuntu as permanent primary boot option:

```
sudo cgpt add -i 6 -P 5 -S 1 /dev/mmcblk0
```

To switch back the primary boot option to ChromeOS while in ChrUbuntu:

```
sudo apt-get install cgpt
sudo cgpt add -i 6 -P 0 -S 1 /dev/mmcblk0
```

In many other guides the device name is `/dev/sda`, however it's only valid if booted into Chrome OS. ChrUbuntu's device name (`mmcblk0` in our case) may be different and could be figured out from `gparted` output:

```
sudo apt-get install gparted
gparted
```

6. Downgrade Chrubuntu Linux kernel, as CUDA support has been removed from actual one (only basic samples can work, e.g. deviceQuery)

```
./cuda-kernel-fix.sh
```
