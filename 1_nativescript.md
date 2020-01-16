# Mobile App <Angular|Nativescript|Android>

## Requirements (Windows)

need more details? let me google that for you

- Install Android Studio (required for app dev with kotlin, java, flutter)
  <https://developer.android.com/studio>
  or just install
  <https://developer.android.com/studio/releases/platform-tools>
  Installation should include Android Drivers, Android SDK, Android Virtual Device

- A USB Cable and a WIFI Connection
  To start debugging on physical device:
  1: Activate developer settings on your mobile phone
  (google that for your specific android OS-version)
  2: Connect via USB (reinstall Android USB-Drivers if necessary)
  <https://developer.android.com/studio/run/device>
  <https://developer.android.com/studio/run/win-usb>

ADB output is:

```bash
    > ~ adb devices
    > List of devices attached
    > R58M71K9NKK     device
```

4: Now you can switch from USB Connection to Wifi Connection via /android/sdk/adb.exe
<https://stackoverflow.com/questions/2604727/how-can-i-connect-to-android-with-adb-over-tcp>

```bash
    > ~ adb tcpip 5556
    restarting in TCP mode port: 5556

    > ~ adb connect 164.356.722.24:5556
    connected to 164.356.722.24:5556
```

Nativescript CLI:

```bash
    > ~ tns devices
Connected devices & emulators
Searching for devices...
iTunes is not installed. Install it on your system and run this command again.
┌───┬─────────────┬──────────┬─────────────────────┬────────┬───────────┬─────────────────┐
│ # │ Device Name │ Platform │ Device Identifier   │ Type   │ Status    │ Connection Type │
│ 1 │ funkzeug    │ Android  │ R58M71K9NKK         │ Device │ Connected │ USB             │
│ 2 │ funkzeug    │ Android  │ 164.356.722.24:5556 │ Device │ Connected │ USB             │
└───┴─────────────┴──────────┴─────────────────────┴────────┴───────────┴─────────────────┘
## Btw the connection type is wrong somehow.. doesnt matter
```

Now you can unplug the USB cable, then you'll see only the latter device in the table...

Want to repeat? Try `adb kill-server`...

## NativeScript

Install NativeScript CLI as global via yarn / npm
Btw. it's a good starting point for the following stuff.. go through the complete setup!
This will take you some time. Get some coffee.
The quick solution described there (one-line install script) is enough if you have already done the android setup ...
`@powershell -NoProfile -ExecutionPolicy Bypass -Command "iex ((new-object net.webclient).DownloadString('https://www.nativescript.org/setup/win'))"`

Now lets create a example project..

```bash
tns create
```

Look inside the project, if you know angular you're welcome..

## Sidekick

From CLI you can do whatever you can do with "Sidekick" (this is the Nativescript GUI)
Its like the Playground online editor compiled to windows .. could be useful for beginners..

## NativeScript CLI

WYSIWYG, check command `tns`

### Remove IOS from project

```bash
tns platform remove ios
# verify with
platform list
# just in case ...
 tns platform add android
```

### Cloud build

```bash
    # Log in with facebook/google/etc OAuth
    tns login

    # Accept EULA
    tns accept eula

    # Cloud build setup environment (Optional)
    tns cloud setup
    ## I had some trouble here:
    ## check `tns extension` if "nativescript-cloud" is already there
    ## otherwise install it with `tns extension install nativescript-cloud@latest`

    ##check your account id
    tns account

    ## build project in the cloud (check with company guideline before sending project sources to the cloud..)
    tns cloud build android --accountId=oOOOooOooO-HAHA-PENG-BLAM-XXXXXXXXXXXXXXX
```

This will give you a link to a downloadable .apk file (.apk = android package format equivalent windows .exe)
mine was `https://livesync.ly/b4qxa3b` .. i've built a virus and sent it to several people
if you navigate there with chrome, you have to accept 2413414 security prompts .. then voila .. app is installed

## Preview APP with QR code

Install "NativeScript Playground app" from PlayStore, then in project folder enter `tns preview`, scan the QR code with "NativeScript Playground app" and see it, attention, this is also hosted somewehere!

## Build Application, Run Application

(check `tns` cli for details)

Equivalent to angular ng serve, you can do

```bash
    ## if you have a device connected
    tns devices
    tns run
    ## This takes some time... (has to build first)
    ## Allow firewall prompt on windows..
```

Voila, this installs "app-debug.apk" on your phone (ofc in developer mode) and opens it. You can see the app there.

You can now edit your code and see the changes live => hot reload mode ...
