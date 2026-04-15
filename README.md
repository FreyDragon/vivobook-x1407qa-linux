# vivobook-x1407qa-linux
<sub>Patches and Devicetree changes to make GNU/Linux excellent on this affordable model!</sub>
<sup>Once completed (100%), I plan to push to mainline changes</sup>
--
Currently using a Vivobook s15 device tree, working on a custom one to fix USB support!
## Feature Matrix

* WIP - Something I am already working on
* TBH - Something I could work on, but not started / no sufficient progress was made
* QC  - Something I cannot work on, depends on Qualcomm's upstream support

| Feature                 | Status | Notes                                                                                                        |
| ----------------------- | -----: | ------------------------------------------------------------------------------------------------------------ |
| Battery Charging        |     ✅ |                                                                                                              |
| Battery Info            |     ✅ | Requires firmware extract                                                                                    |
| Bluetooth               |     ✅ |                                                                                                              |
| Iris/HW decoder         |    TBH | Will not work, due to this being a Purwa device                                                              |
| Camera                  |    TBH | Will NOT work, due to this being a Purwa device                                                              |
| Display                 |     ✅ | FHD OLED and LCD on UX3407QA, 3K OLED on UX3407RA                                                            |
| GPU Acceleration        |     ✅ | Requires firmware extract                                                                                    |
| Keyboard                |     ✅ |                                                                                                              |
| Microphone              |     ✅ |                                                                                                              |
| NVMe                    |     ✅ |                                                                                                              |
| Speakers                |     ✅ | ~Requires userland configuration, see below.~ Works with latest upstream alsa-ucm-config, linux-firmware     |
| Audio Jack              |     ✅ |                                                                                                              |
| Suspend                 |    WIP | Suspends tolerably, lid switch working, but fan stays on. Power drop in sleep isn't best, nothing I can fix. |
| Touchpad                |     ✅ |                                                                                                              |
| TPM                     |     ❌ | Firmware TPM                                                                                                 |
| USB-A 3.0               |    WIP | Requires devicetree work for hotplug to function (coldplugs fine)                                            |
| USB-C 3.0               |    WIP | Requires devicetree work for hotplug to function (coldplugs fine)                                            |
| USB-C Booting           |     ✅ |                                                                                                              |
| USB-C DP Alt Mode       |    WIP | Requires firmware extract                                                                                    |
| USB-C DP over dock      |    WIP |                                                                                                              |
| HDMI                    |    WIP |                                                                                                              |
| Wi-Fi                   |     ✅ | Requires firmware extraction and patching.                                                                   |
| EC                      |     ❌ | Similar to out-of-tree EC driver for Lenovo Slim 7x.                                                         |


# Credits
 https://github.com/alexVinarskis/linux-x1e80100-zenbook-a14 
<small>Feature Matrix Template, Initial Inspiration, Contains 90% of the work to make this model work.</small>
 https://github.com/aarch64-laptops
<small>Made the MAJORITY of the devicetree</small>
