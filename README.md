# Open re-implementation of the Quansheng UV-K5/K6/5R v2.1.27 firmware

This repository is a fork of[Egzumer custom firmware](https://github.com/egzumer/uv-k5-firmware-custom), who was a merge of [OneOfEleven custom firmware](https://github.com/OneOfEleven/uv-k5-firmware-custom) with [fagci spectrum analizer](https://github.com/fagci/uv-k5-firmware-fagci-mod/tree/refactor) plus my few changes.

All is a cloned and customized version of DualTachyon's open firmware found [here](https://github.com/DualTachyon/uv-k5-firmware) ... a cool achievement !

> [!WARNING]
> EN - Use this firmware at your own risk (entirely). There is absolutely no guarantee that it will work in any way shape or form on your radio(s), it may even brick your radio(s), in which case, you'd need to buy another radio.
Anyway, have fun.
>
> _FR - Utilisez ce firmware à vos risques et périls. Il n'y a absolument aucune garantie qu'il fonctionnera d'une manière ou d'une autre sur votre (vos) radio(s), il peut même bousiller votre (vos) radio(s), dans ce cas, vous devrez acheter une autre radio. Quoi qu'il en soit, amusez-vous bien._

> [!CAUTION]
> EN - I recommend to backup your eeprom with [k5prog](https://github.com/sq5bpf/k5prog) before playing with alternative firmwares. It's a good reflex to have. 
>
> _FR - Je recommande de sauvegarder votre eeprom avec [k5prog](https://github.com/sq5bpf/k5prog) avant de jouer avec des firmwares alternatifs. C'est un bon réflexe à avoir._

# Donations

Special thanks to Jean-Cyrille F6IWW, Fabrice 14RC123, David F4BPP, Olivier, Frédéric F4ESO and Stéphane F5LGW for their [donations](https://www.paypal.com/paypalme/F4HWN). That’s so kind of them. Thanks so much 🙏🏻

## Table of Contents

* [My Features](#main-features)
* [Main Features from Egzumer](#main-features-from-egzumer)
* [Manual](#manual)
* [Radio Performance](#radio-performance)
* [Compiler](#compiler)
* [Building](#building)
* [Credits](#credits)
* [Other sources of information](#other-sources-of-information)
* [License](#license)
* [Example changes/updates](#example-changesupdates)

## Main features:

* improve default power settings level (Low ~125mW, Mid ~2W and High ~5W),
* improve s-meter (IARU recommandations),
* improve UI: 
    * menu index, 
    * s-meter design, 
    * MAIN ONLY screen mode, 
    * DUAL and CROSS screen mode, 
    * RX blink on VFO RX, 
    * RX LED blink, 
    * Squelch level and Monitor,
    * Step value,
    * CTCSS or DCS value,
    * KeyLock message,
    * and more...
* new menu entries:
    * add SetLow menu to set low power (<20mW, 125mW, 250mW, 500mW and 1W),
    * add SetPtt menu to set PTT mode (Classic or OnePush),
    * add SetTot menu to set TOT alert (Off, Sound, Visual, All),
    * add SetCtr menu to set contrast (0 to 15),
    * add SetInv menu to set screen in invert mode (Off or On),
    * add SetEot menu to set EOT (End Of Transmission) alert (Off, Sound, Visual, All),
    * add SetMet menu to set s-meter style (Classic or Tiny),
    * add SetLck menu to set what is locked (Keys or Keys + PTT),
    * add SetGui menu to set font size on the VFO baseline (Classic or Tiny),
    * improve PonMsg menu,
* improve status bar,
    * add SetPtt mode in status bar,
    * change font and bitmaps,
* new actions:
    * SWITCH RxMode, 
    * SWITCH PTT, 
    * SWITCH WIDE NARROW,
    * 1750Hz,
    * BlMin Tmp Pff,
* new key combinations:
    * add the F + UP or F + DOWN key combination to dynamically change the Squelch level,
    * add the F + F1 or F + F2 key combination to dynamically change the Step,
* many fix:
    * squelch, 
    * s-meter,
    * DTMF overlaying, 
    * scan list 2 ignored, 
    * scan range limit,
    * and more...
* enabled ENABLE_CTCSS_TAIL_PHASE_SHIFT,
* enabled ENABLE_BLMIN_TMP_OFF,
* disabled ENABLE_DTMF_CALLING,
* disabled SCRAMBLER,
* unlock TX on all bands needs only to be repeat 3 times,
* and more...

## Main features from Egzumer:
* many of OneOfEleven mods:
   * AM fix, huge improvement in reception quality
   * long press buttons functions replicating F+ action
   * fast scanning
   * channel name editing in the menu
   * channel name + frequency display option
   * shortcut for scan-list assignment (long press `5 NOAA`)
   * scan-list toggle (long press `* Scan` while scanning)
   * configurable button function selectable from menu
   * battery percentage/voltage on status bar, selectable from menu
   * longer backlight times
   * mic bar
   * RSSI s-meter
   * more frequency steps
   * squelch more sensitive
* fagci spectrum analyzer (**F+5** to turn on)
* some other mods introduced by me:
   * SSB demodulation (adopted from fagci)
   * backlight dimming
   * battery voltage calibration from menu
   * better battery percentage calculation, selectable for 1600mAh or 2200mAh
   * more configurable button functions
   * long press MENU as another configurable button
   * better DCS/CTCSS scanning in the menu (`* SCAN` while in RX DCS/CTCSS menu item)
   * Piotr022 style s-meter
   * restore initial freq/channel when scanning stopped with EXIT, remember last found transmission with MENU button
   * reordered and renamed menu entries
   * LCD interference crash fix
   * many others...

 ## Manual

Up to date manual is available in the [Wiki section](https://github.com/egzumer/uv-k5-firmware-custom/wiki)

## Radio performance

Please note that the Quansheng UV-Kx radios are not professional quality transceivers, their
performance is strictly limited. The RX front end has no track-tuned band pass filtering
at all, and so are wide band/wide open to any and all signals over a large frequency range.

Using the radio in high intensity RF environments will most likely make reception anything but
easy (AM mode will suffer far more than FM ever will), the receiver simply doesn't have a
great dynamic range, which results in distorted AM audio with stronger RX'ed signals.
There is nothing more anyone can do in firmware/software to improve that, once the RX gain
adjustment I do (AM fix) reaches the hardwares limit, your AM RX audio will be all but
non-existent (just like Quansheng's firmware).
On the other hand, FM RX audio will/should be fine.

But, they are nice toys for the price, fun to play with.

## Compiler

arm-none-eabi GCC version 10.3.1 is recommended, which is the current version on Ubuntu 22.04.03 LTS.
Other versions may generate a flash file that is too big.
You can get an appropriate version from: https://developer.arm.com/downloads/-/gnu-rm

clang may be used but isn't fully supported. Resulting binaries may also be bigger.
You can get it from: https://releases.llvm.org/download.html

## Building

### Github Codespace build method

This is the least demanding option as you don't have to install enything on your computer. All you need is Github account.

1. Go to https://github.com/egzumer/uv-k5-firmware-custom
1. Click green `Code` button
1. Change tab from `Local` to `Codespace`
1. Click green `Create codespace on main` button

<img src="images/codespace1.png" width=700 />

5. Open `Makefile`
1. Edit build options, save `Makefile` changes
1. Run `./compile-with-docker.sh` in terminal window
1. Open folder `compiled-firmware`
1. Right click `firmware.packed.bin`
1. Click `Download`, now you should have a firmware on your computer that you can proceed to flash on your radio. You can use [online flasher](https://egzumer.github.io/uvtools)

<img src="images/codespace2.png" width=700 />

### Docker build method

If you have docker installed you can use [compile-with-docker.bat](./compile-with-docker.bat) (Windows) or [compile-with-docker.sh](./compile-with-docker.sh) (Linux/Mac), the output files are created in `compiled-firmware` folder. This method gives significantly smaller binaries, I've seen differences up to 1kb, so it can fit more functionalities this way. The challenge can be (or not) installing docker itself.

### Windows environment build method

1. Open windows command line and run:
    ```
    winget install -e -h git.git Python.Python.3.8 GnuWin32.Make
    winget install -e -h Arm.GnuArmEmbeddedToolchain -v "10 2021.10"
    ```
2. Close command line, open a new one and run:
    ```
    pip install --user --upgrade pip
    pip install crcmod
    mkdir c:\projects & cd /D c:/projects
    git clone https://github.com/egzumer/uv-k5-firmware-custom.git
    ```
3. From now on you can build the firmware by going to `c:\projects\uv-k5-firmware-custom` and running `win_make.bat` or by running a command line:
    ```
    cd /D c:\projects\uv-k5-firmware-custom
    win_make.bat
    ```
4. To reset the repository and pull new changes run (!!! it will delete all your changes !!!):
    ```
    cd /D c:\projects\uv-k5-firmware-custom
    git reset --hard & git clean -fd & git pull
    ```

I've left some notes in the win_make.bat file to maybe help with stuff.

## Credits

Many thanks to various people:

* [Egzumer](https://github.com/egzumer)
* [OneOfEleven](https://github.com/OneOfEleven)
* [DualTachyon](https://github.com/DualTachyon)
* [Mikhail](https://github.com/fagci)
* [Andrej](https://github.com/Tunas1337)
* [Manuel](https://github.com/manujedi)
* @wagner
* @Lohtse Shar
* [@Matoz](https://github.com/spm81)
* @Davide
* @Ismo OH2FTG
* [OneOfEleven](https://github.com/OneOfEleven)
* @d1ced95
* and others I forget

## Other sources of information

[ludwich66 - Quansheng UV-K5 Wiki](https://github.com/ludwich66/Quansheng_UV-K5_Wiki/wiki)<br>
[amnemonic - tools and sources of information](https://github.com/amnemonic/Quansheng_UV-K5_Firmware)

## License

Copyright 2023 Dual Tachyon
https://github.com/DualTachyon

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.

## Example changes/updates

Here are a few photos.

|![SetPtt Option](https://github.com/armel/uv-k5-firmware-custom-feat-F4HWN/blob/main/photos/IMG_3080.jpeg)|
|:--:|
| SetPtt Option |


|![Dual RX Respond](https://github.com/armel/uv-k5-firmware-custom-feat-F4HWN/blob/main/photos/IMG_3082.jpeg)|
|:--:|
| Dual RX Respond |


|![Main Only](https://github.com/armel/uv-k5-firmware-custom-feat-F4HWN/blob/main/photos/IMG_3081.jpeg)|
|:--:|
| Main Only |


|![Main TX Dual RX](https://github.com/armel/uv-k5-firmware-custom-feat-F4HWN/blob/main/photos/IMG_3079.jpeg)|
|:--:|
| Main TX Dual RX |