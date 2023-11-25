# TotKSteamDeckGuide

## Target Audience

This guide is designed for anyone looking to play Tears of the Kingdom (Or any other Switch game) on their Steam Deck. I was requested to provide a guide as a response to a YouTube video.

## Disclaimer

This guide is presented as is. There is no legal precedent that actually protects the use of de-encryption tools and emulators (See this [video](https://www.youtube.com/watch?v=wROQUZDCIMI) by Moon Channel breaking down the legal history of Emulation). Some of the actions being taken could lead to an account ban on your Switch if you are not careful enough. Following the instructions exactly SHOULD (Key word) keep you safe from any hardware bans, but this is always a risk when modifying proprietary hardware. I take no responsibility should you choose to follow this guide and your system winds up getting banned.

## Requirements

This guide was written the following items in mind. Anything marked with an asterisk is required.

```
* Switch vulnerable to the fusee-galee exploit running firmware HOS 17.0.0 - https://ismyswitchpatched.com/
* Copy of Tears of the Kingdon (Nintendo E-Shop copy or physical copy, this guide is written with an E-Shop copy in mind)
* RCM Jig - https://www.amazon.com/Connector-Nintendo-Recovery-Archive-Simulator/dp/B089YDF9N1/?th=1
* microSD for the Switch at least 64GBs in size - larger is recommended
* USB to microSD reader to plug into your desktop PC
* USB-A to USB-C cable capable of data transfer
* Desktop PC running Linux (Or Windows, though this guide is written with Arch Linux in mind)
* Steam Deck (Any model)
  microSD for the Steam Deck (Recommended 256GB+ with A2 spec)
```

## Prepare the Switch microSD

Before continuing, it is likely best to format your SD card using the exFAT file system. Do note that formatting the microSD will erase any data on it. This normally just includes installed games as save data is normally just on the Switch's eMMC storage.

### Formatting

Your Switch should be able to handle this by going into `System Settings`:
![20231123_084722](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/8d3e40ab-5e16-48bb-b788-89570def4b35)

Scrolling down to `System`, then down to `Formatting Options`:
![20231123_084821](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/35046b17-51f8-4a42-846f-57d61e1ae7ce)

Selecting `Format microSD Card`:
![20231123_084857](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/20d38b2f-bd2f-44f5-a246-240f24387561)

Then `Continue`:
![20231123_084945](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/ed6d0352-deeb-4a6f-a3d5-98ed4a543c9e)

Finally `Format`:
![20231123_085007](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/2a76b03b-7d2e-4165-a80d-18d817097d81)

### Install TotK and Update

Either insert your TotK physical cartridge or download the game from the E-Shop, then attempt to run it once in order to update it. If you are using an E-Shop version and it does not appear on your main menu, you can open the E-Shop and select your profile icon:
![20231123_090321](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/dc38ecf2-1189-4f8d-9475-2b02952c6f43)

Once in the `Account Information` page go down to `Redownload`, then scroll through the list of games to find TotK and start the re-download.
![20231123_090415](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/0a31c36e-2cf3-434c-b6ee-902d9221c5c3)

### PC Setup

#### sd Folder

Now that we have the microSD connected to our PC we need to prepare all of our files to jailbreak the Switch. I recommend visiting this [page](https://www.sdsetup.com/console?switch) to get the basis of the files you need. This page is out of date, so we will need to manually get some newer packages. First, select `Recommended Defaults`:
![Screenshot_20231123_090955](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/1d33c6de-b1f0-4179-a79e-be007df55739)

Then scroll down to the bottom and select your desired PC tools (In my case, I'm using Linux so I select `fusee-launcher`. Windows users will want `TegraRcmGUI`) and then select `Download your ZIP`:
![Screenshot_20231123_090955](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/df2c5da6-cb7c-4daa-8aeb-a1a5a5a30224)

Extract the .zip file and you should have 3 folders inside, `pc`, `sd`, and `payloads`. We want to open up the `sd` folder and delete the `atmosphere` folder and the `hbmenu.nro` application.
![Screenshot_20231123_091845](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/bc85caff-c20c-42fc-90de-97fb1036d3f5)

##### Atmosphere

Since we just removed our custom firmware `Atmosphere`, we want to replace it with an up to date version. Navigate to their [releases](https://github.com/Atmosphere-NX/Atmosphere/releases) GitHub page and grab the most recent .zip archive. Open the archive and extract the files into the `sd` folder:
![Screenshot_20231123_092116](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/5bb86b0e-7695-409a-84c9-aff6a81977b9)

Ensure that you overwrite any files and folders if prompted.
![Screenshot_20231123_092434](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/7a8ad1b5-9ad3-4714-950a-78daa137e119)

##### Hekate

Next we need to update our custom bootloader, `Hekate`. The version shipped with the `sdsetup` page is out of date and won't work on newer firmware. Unlike the `Atmosphere` update, we do not need to delete any files or folders. We can just grab the most recent .zip archive from their [releases](https://github.com/Atmosphere-NX/Atmosphere/releases) page, then extract the files into the `sd` folder, overwriting when necessary:
![Screenshot_20231123_092908](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/f42e7855-7153-4499-9392-27e93c42d5d4)

Next we want to move the `hekate_ctcaer_x.x.x.bin` file into the `./sd/bootloader/payloads/` folder:
![Screenshot_20231123_093059](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/7172f209-52d0-4c8e-9137-07bf73d9c45f)

We also want to go into the `./sd/bootloader/payloads` folder, rename `reboot_payload.bin` to `reboot_payload_bak.bin`, copy `hekate_ctcaer_x.x.x.bin` into this folder, and rename it to `reboot_payload.bin`. This will allow us to reboot into our bootloader from our custom firmware, instead of having to reconnect the Switch to a PC and re-inject the payload later.
![Screenshot_20231123_093510](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/73cc758d-41df-4616-bda4-67e82b31a080)

##### Lockpick RCM

We also want to grab the Lockpick RCM utility. Unfortunately, Nintendo issued a DMCA takedown of this tool so I can't provide a direct link to it. There are still binaries that exist out on the internet, but I would rather not test Nintedo's ninja lawyers by providing a direct link. You will be on your own finding this one.

Once you have the `Lockpick_RCM.bin` file you will want to place it in the `./sd/bootloader/payloads/` folder:
![Screenshot_20231123_093915](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/d60093af-377c-4161-8836-37e98d60c7c2)

##### NX Dump Tool

Finally, we will need a tool capable of "dumping" our game contents for use in an emulator. I recommend the `NX Dump Tool` since it is relatively easy to use and can dump directly to your PC via a USB-C cable and the `NX Dump Client` utility. You can download the most recent `nxdt_rw_poc.nro` file at their [releases](https://github.com/DarkMatterCore/nxdumptool/releases) page. Once you have it, simply place it under the `./sd/switch/` folder. You can also remove the old folder titled `nxdumptool` as this is an older version that does not function with the newest firmware:
![Screenshot_20231123_094531](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/ec97010c-0d8e-4c97-b3e1-726950c5237d)

Now would also be a goood time to install the `NX Dump Client` utility. On Linux, this can be installed via Flatpak:
![Screenshot_20231123_094801](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/4d009c78-b4c3-4b48-8335-78e053abd420)

You will also need to perform a first time setup by creating a udev rule. Normally you will get a popup when you first run the proogram instructing you to enter the following command in your terminal:
```bash
flatpak run org.v1993.NXDumpClient --print-udev-rules | sudo sh -c 'cat > /etc/udev/rules.d/71-nxdumptool.rules'
```
Once this is done you can restar the application and it will be ready to receive dumped games directly from your Switch.

#### pc Folder (Linux)

Next we want to copy `hekate_ctcaer_x.x.x.bin` to the `./pc/fusee-launcher/` folder.

This is all the prep we need to do with the folder itself, but you do need to make sure you have `python` v3 and `python-pyusb` installed. On Arch Linux we would run:
```bash
sudo pacman -S python python-pyusb
```

#### pc Folder (Windows)

TODO

## Hacking the Switch

### Custom DNS Entries

We're finally ready to jailbreak our Switch. Ensure TotK has finished downloading. Before shutting the Switch down, we want to set up custom DNS entires to prevent our Switch from communicating with Nintedo servers while we are running our Jailbreak. This isn't 100% necessary, but is a great safety step to ensure you don't do anything to accidentally get your Switch banned while running custom firmware.

To start, navigate to `System Settings`:
![20231123_095555](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/b45f1eda-5fe3-4ae8-b709-47c4bbd40e0d)

Then `Internet` and `Internet Settings`:
![20231123_095809](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/0fe081e2-6086-4ebc-8c43-a96d29b67dbe)

Select your network (In my case, `DP-Wifi`):
![20231123_095903](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/f8f0f9aa-0af9-4e35-9e14-3eb115fe1f51)

Next select `Change Settings`:
![20231123_095951](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/53e95ca2-847b-4fdb-8fc0-b0896c6c8eea)

Finally, scroll down to `DNS Settings`, change to `Manual`, and enter `163.172.141.219` for your `Primary DNS` and `207.246.121.077` for your Secondary DNS:
![20231123_100016](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/9ac862f6-c025-451f-a035-b8a29260dbc2)

If you are in the EU, you may want to swap these around.

Save your settings and exit. You can now toggle on your custom DNS servers by changing your `DNS Settings` to `Manual`, or turn them off by changing them back to `Automatic`. It is important to note that these changes will not take affect until your next reboot, and while they are active you can not communicate with any Nintendo servers (E-Shop, Cloud Saves, Update Checks, etc).

### Copying files to the microSD Card

Power down your Switch entirely and remove your microSD card, then insert it to your PC.

All you need to do now is copy all the files and folders from `./sd/` to the root of your Switch's microSD (not into the `Nintendo` folder):
![Screenshot_20231123_100659](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/4d093242-c8bc-48bc-b782-6a50489822d3)

Once all the files are copied, eject the microSD from your PC and reconnect it to your Switch. Do not turn your Switch back on yet.

### Entering RCM

Now it's finally time to perform our jailbreak. The exploit we are relying upon is a flow in the Tegra chip made by Nvidia for the Nintendo Switch called `fusee-gelee`. This is a hardware exploit and can not be patched via software, which is why older Switch models are still vulnerable and will never be fixed. Using `fusee-galee` we can press a certain combination of buttons that tells the Switch to start in `RCM` (**R**e**C**overy **M**ode), a failsafe Nvidia created for diagnosis and recovery tools. The easiest way to do this is ensure that your Switch is completely powered down, remove the right JoyCon, and slide your RCM Jig down the right JoyCon Rail:
![20231123_101416](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/d2b23ea7-5a9b-4d1c-b9e4-d6d133345639)

Once your RCM Jig is in place, you will want to do a short press down on the `Volume+` and `Power` Buttons at the same time:
![20231123_101526](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/4800ede2-2bed-4120-8366-23771c601747)

If you have done everything right, it should appear as if nothing happened. The screen should stay black, and you should not be able to power on the Switch by tapping the `Power` button. This would mean your Switch has entered `RCM` and is ready to receive a payload from your PC.

### Injecting the Payload (Linux)

Now that your Switch is in `RCM` we want to connect it to our PC via a USB-C cable. Once we have that, naviage to the `./pc/fusee-launcher/` folder and open a terminal there:
![Screenshot_20231123_101831](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/4cb569b0-0343-496c-bde3-63836e73cc05)

In the terminal, enter the following:
```bash
sudo python fusee-launcher.py hekate_ctcaer_6.0.7.bin
```

If everything worked, you should receive an output like shown here:
![Screenshot_20231123_102137](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/676e3143-d955-4b95-bb77-971eec73ac8b)

### Dumping BIOS Keys

Your Switch should now be booted into the `hekate` bootloader. It should ask you to set a date and time. This will not affect the actual hardware clock.

On the `heakte` home page, select `Paylods`:
![20231123_102607-payloads](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/5cf9bf2a-a4b3-499c-a2ad-2852929070f6)

Then select `Lockpick_RCM.bin`:
![20231123_102640](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/9a722f47-4b65-465a-a8c0-67aa9d497d0d)

Once inside of `Lockpick RCM` you will use the `Volume+` and `Volume-` buttons to navigate up and down, and the `Power` button as "Select". Select `Dump from SysNAND`:
![20231123_103224](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/87f9392a-f985-4f99-a817-e1e28d113dd3)

This should spit out a screen that looks like the following:
![20231123_103112](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/5bab6411-67df-493f-b252-20959a2e7596)

Once you have dumped your keys, hit the `Power` button to go back to the main menu, then select `Reboot to Hekate`:
![20231123_103447](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/abc8455a-6155-4b5d-a049-d4394b7e7473)

## Boot into Atmosphere

Now that we're back in Hekate, it's time to boot into our custom firmware `Atmosphere`. Select `Launch`:
![20231123_102607-launch](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/b95e2d4e-c1f2-45fc-ac52-a55afa8615e7)

Then select `CFW (SysMMC)`:
![20231123_103539](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/10734062-525d-46ca-addd-50013fde6090)

This will boot into what looks like a standard SwitchOS. You will want to remove the RCM Jig and reconenct your right JoyCon next.

### Dumping Firmware Files

Select any installed title from the main menu, hold down `R1`, then press `A`. Keep holding down `R1` and attempt to launch the game. If you are syncing cloud storage you may get an error, simply select `Launch Anyways`. If everything was done right, you should be taken to our Homebrew Loader. On this menu, scroll over and select `Goldleaf`:
![20231123_104138](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/97a2f9d8-a424-4afe-8710-fcade0ddc3af)

Inside of `Goldleaf` select `Explore content`:
![20231123_104310](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/c6a2f9de-8b36-40eb-b8e0-8f9ac851007c)

Next select `Console Memory (SYSTEM)`:
![20231123_104357](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/2e034484-042c-46fb-83cc-51fc9ba3d4ee)

Then `Contents`:
![20231123_104435](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/31a013bd-e22a-4b9f-b163-4d8199317820)

And finally highlight `Reigstered`:
![20231123_104613](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/30082fa1-7673-4d6a-85f7-8f46ef862749)

Once highlighted press the `Y` button, and then select `Copy`:
![20231123_104722](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/25cfdd71-998e-4cc1-bb41-ce61c83df423)

Once copied, back out all the way to the root directory and select `SD card`:
![20231123_104829](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/454fbf87-b59f-41c6-baf1-6ed7ac9e16c3)

Inside the SD card press the `X` button to paste the `registered` folder and then select `Yes`:
![20231123_104933](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/c946f8f9-b605-41d5-aae4-546bf418f368)

Once the copy finishes, hit the `Home` button, highlight the "running software", and press the `X` button to close it.

### Dumping Content

We are finally ready to dump our game content for use on our Steam Deck. Highlight an installed game and re-enter the homebrew menu by holding down `R1` and pressing the `A` button. Keep holding `R1` as you click through the errors. Once in the homebrew menu we want to select `nxdt_rw_poc`:
![20231123_105427](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/22938db0-ef29-488d-8e02-cf2018d6a699)

#### Gamecard Dumping (.xci)

If your game is installed on a cartride you can dump the game as a .xci. Do note that my game is not installed via a cartridge, so I will instead be dumping Mario Party Superstars.

Select `gamecard menu` then `dump gamecard image (xci)`.

Ensure all options are set to `no` and that the `output storage` is set to `usb host (pc)`:
![20231123_105816](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/d97329c0-56ac-4390-9f03-5ca163a131a6)

At this time you will want to make sure you have `NX Dump Client` running on your PC and that it shows a connected device:
![Screenshot_20231123_105856](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/5dd1be97-0b7e-4b40-ba76-29a295575efb)

You can now select `start xci dump`. This will take a few minutes.

#### E-Shop Ttie Dumping (.nsp)

If your game is installed via the E-Shop you can dump the game as a .nsp.

Select `user titles menu` then select your game. In this case `The Legend of Zelda: Tears of the Kingdom`. Next select `nsp dump options` then `dump base application`.

Ensure all options match the following image and that the `output storage` is set to `usb host (pc)`:
![20231123_110845](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/255f9b35-8a6d-4bda-a709-376dd402cde7)

At this time you will want to make sure you have `NX Dump Client` running on your PC and that it shows a connected device:
![Screenshot_20231123_105856](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/5dd1be97-0b7e-4b40-ba76-29a295575efb)

You can now select `start nsp dump`. This will take a few minutes.

#### Update Dumping

Updates are dumped as .nsp files regardless of if it is gamecard content or E-Shop content.

Select `user titles menu` then select your game. In this case `The Legend of Zelda: Tears of the Kingdom`. Next select `nsp dump options` then `dump update`.

Ensure all the options match the following image and that `output storage` is set to `usb host (pc)`:

At this time you will want to make sure you have `NX Dump Client` running on your PC and that it shows a connected device.
![Screenshot_20231123_105856](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/5dd1be97-0b7e-4b40-ba76-29a295575efb)

You can now select `start nsp dump`. This should only take a few seconds.

#### DLC Dumping (Not currently necessary for TotK)

DLC files are dumped as .nsp files regardless of if it is gamecard content or E-Shop content.

Select `user titles menu` then select your game. In this case `The Legend of Zelda: Tears of the Kingdom`. Next select `nsp dump options` then `dump dlc`.

Ensure all the options match the following image and that `output storage` is set to `usb host (pc)`:
![20231123_110845](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/bdc20fe9-4c2d-4fa7-919f-cbd5907831b3)

At this time you will want to make sure you have `NX Dump Client` running on your PC and that it shows a connected device.
![Screenshot_20231123_105856](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/5dd1be97-0b7e-4b40-ba76-29a295575efb)

You can now select `start nsp dump`. This should only take a few seconds.

### Extracting Keys and Firmware

Now that we have the games dumped we still need to extract the BIOS keys and firmware files we dumped earlier. Hold down the power button on the Switch until you get the option to restart. Restart the Switch and you should be taken back to Hekate bootloader.

In Hekate, select `Tools`:
![20231123_102607-tools](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/60ad16d7-6bdc-4087-9460-2847d8aca4ff)

Then select `USB Tools`:
![20231123_113030](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/e8309c89-7725-4fa0-9ed4-2c119486188c)

Finally select `SD Card`:
![20231123_113120](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/cc77e369-1625-4b12-9fc0-5ebe53cfaf7e)

This will mount the SD card do your PC where we can copy the `registered` folder (firmware files) along with the `./switch/title.keys`, `./switch/prod.keys`, and `./switch/dev.keys` files (BIOS keys) to somewhere safe on our PC:
![Screenshot_20231123_113333](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/193d23fe-07f0-47ba-b35e-85786998a33f)

## Steam Deck Setup

Ok, so we're done with the Switch and the messy pictures taken from my phones camera. From here on out we will exclusively be using the Steam Deck and PC.

### Switch to Desktop Mode

Hit the `Steam` button and scroll down to `Power`:
![steamuserimages-a akamaihd](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/5baa1aba-fcde-47bc-bf51-479ba499d3d6)

In the power menu, select `Switch to Desktop`:
![steamuserimages-a akamaihd-2](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/54171b80-3892-485e-8b30-5266d44f3273)

This will drop us into the KDE Plasma Desktop Environment.

### Install AnyDesk

To make our desktop experience easier, we're going to use the `AnyDesk` screen sharing application to control our Steam Deck from our PC.

Open the `Discover App Store`:
![Screenshot_20231123_115728](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/3b3d0bb0-81f3-4de2-ad6b-2918ca520e35)

Navigate to the `Search Field`. Click into it and press `Steam` + `X` to open the on screen keyboard, then search for `anydesk` and click `Install`:
![Screenshot_20231123_115950](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/e5e06930-c693-43be-a0bd-cf34ee3267b2)

Once AnyDesk has finished installing, click anywhere on the software except `Remove`, then click `Launch`:
![Screenshot_20231123_120201](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/82cf5400-a354-4b8a-acba-6693c98f4574)
![Screenshot_20231123_120237](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/9c8d3c51-4746-4226-b226-0742f0d25e76)

Go to the `New Session` tab and take note of your systems address (Should look like `1 123 456 789`).

Open `AnyDesk` on your PC and connect to the Steam Deck's address.

A new window will pop up in the background on your Steam Deck. You can focus it by clicking on the `AnyDesk` icon on your task bar to accept the connection.

### Install Firefox (Possibly Optional)

Now that we have access to a mouse and keyboard, click on the `FireFox` icon on your task bar. If `FireFox` is not already installed, this will open up the page in the app store to install `FireFox`:
![Screenshot_20231123_120644](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/5b06515b-afd8-4f3d-9830-029a3c88296f)

### Install EmuDeck

Once FireFox is installed, launch it and navigate to EmuDeck's install page: https://www.emudeck.com/#download

Make sure you select the `SteamOS` option:
![Screenshot_20231123_120828](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/85d3cfd2-c2e9-42dc-9c6b-050353616a27)

Once downloaded, open the containing folder:
![Screenshot_20231123_120925](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/8495b941-1569-4e3c-bad1-8384b2d2542b)

Then double left click on the `EmuDeck.dkestop.download` icon:
![Screenshot_20231123_121007](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/d79c7740-482f-4e7d-ab22-09eb2fe109e3)

Select `Execute`, then `Continue`. This will open the EmuDeck Installer. Select `Custom Mode`, then select your install location (In my case, my microSD). Make sure you select the `Steam Deck` option, and disable/enable the emulators you want. I recommend keeping `RyuJinx` disabled and enabling `Yuzu`. `RyuJinx` is generally more accurate, but `Yuzu` tends to perform better, especially on lower power devices.

Navigate through the rest of the settings and select your desired options (I/E, Auto Saves with RetroArch, screen sizes, bezels, etc). Let the software finish installing, and you should be brought to a page that looks like this:
![Screenshot_20231123_121857](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/01668732-36c5-41d1-ae97-64db5a50c699)

We're going to `Skip for now`.

At this point, we need to get all of our files from our PC (ROM, update file, BIOS keys, and firmware) to the Steam Deck. There are various ways you can do this, and I'm not going to go into detail. For context, I have a local file server (NAS, Network Attached Storage) where I save all my ROMs and emulation files such as firmware and BIOS keys. Any device on my local network (Including my Steam Deck) can access this, so you will see me copying files from this local server.

#### BIOS Keys

First we want to copy over our BIOS keys. Copy the files into the `$(emulation)/bios/yuzu/keys/` folder:
![Screenshot_20231123_122330](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/30af5711-3f08-4999-9d07-e1bf78ebd7a8)

#### Firmware Files

Next we also want to copy the firmware files. Most games do not require firmware, but TotK requires at least version 16 or later. We should be copying over version 17.0.0 into the `$(emulation)/bios/yuzu/firmware/` folder:
![Screenshot_20231123_122509](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/00f1b301-592d-4947-9be2-3fc31789f95c)

#### ROM File

Now we have to copy over the ROM file into the `$(emulation)/roms/switch/` folder:
![Screenshot_20231123_122809](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/6b58c98e-c8ae-4d0e-96d4-52dcddb7b11e)

#### Update File

Finally, we want to copy over our update so we can install it within the `Yuzu` emulator. Copy the update file to the `Downloads` folder:
![Screenshot_20231123_124259](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/3a2be838-5e39-4eda-a3ef-cf2e910692c5)

##### Install the Update

Moving over the update file does nothing on it's own. We need to launch Yuzu and install it. Open the start menu and launch the `Yuzu` appimage. You may get an error regarding firmware decryption. I'm not sure why I was getting this error, but it did not prevent me from continuing.

You should see Tears of the Kingdom in your game list. Before proceeding, we want to install our update if it was not already packaged with a .xci file. Select `File` then `Install Files to NAND`:
![Screenshot_20231123_124026](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/581fef04-c2f3-4fa5-98f2-69b1c40d0c82)

Next navigate to your `Downlaods` folder and select the update file, then `Install`:
![Screenshot_20231123_124517](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/fa630e68-5b44-4850-9ca5-b05bf1082bbe)

#### Stean ROM Manager

Now that we have everything in place we want to run `Steam ROM Manager` to add our game to Steam. Open the `EmuDeck` app via your app launcher (Start Menu) and select `Launch` under `Steam ROM Manager`:
![Screenshot_20231123_124751](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/8110bbf4-efd7-4290-bb53-d37271267204)

This will give you a popup asking if you would like to exit Steam. Click `Yes`.

Once `Steam ROM Manager` launches, I recommend going into `Settings` and changing to the `Deck` theme:
![Screenshot_20231123_124922](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/999e7df8-9125-4b29-8d13-5a91e966608e)

I recommend disabling the `EmulationStation` parser first.

Next select the `Preview` menu, then select `Parse`:
![Screenshot_20231123_125039](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/1a07a311-7db3-49da-94c4-8265e11a3f58)

This will then look through your Emulation folder and grab all the necessary ROMs. Change the `Artwork` from `Portraits` to `All Artwork`, then select some artwork that hasn't been DMCA'ed by Nintendo yet. Once you have selected all your artwork, click on `Save to Steam`:
![Screenshot_20231123_125503](https://github.com/Halornek/TotkSteamDeckGuide/assets/7231881/f46c5afd-4e09-434f-b1c4-801ba11a80bb)

### Play your Switch Game

And now we're done. At least with the basic setup. Most Switch games will just simply work now. Some may require tweaking or mod support. For the meantime, you can boot back into `Game Mode` by selecting `Return to Gaming Mode` on your desktop.

TotK may have some stutters while compiling shaders. This tends to resolve itself the more you play the game.

### Mods (Optional)

TBD: Mods not yet compiled for 1.2.1.
