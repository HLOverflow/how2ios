# Set up

## Jailbreak

Macbook version 10.13.6 

1. register an apple id account
Visit https://appleid.apple.com/#!&page=signin

```
Note: Never ever update/upgrade the iphone device.
iphone version: 11.1.2
Exploit: Electra ipa from electra website by coolstar. ( sha1: 1b35c1364c791aeceab2ded5f04e74bf27d131b1 )
Method: Use Cydia Impactor ( http://www.cydiaimpactor.com )
```

Open cydia impactor. 

Connect iphone to macbook by lightning-to-usb cable.

Drap-and-drop the Electra IPA onto the Impactor's GUI interface.

Login with username and password of apple id account.

Once complete, plug off the lightning-to-usb cable.

Visit settings -> general -> Device Management ( with your account ) -> "trust" the email account.

Turn on airplane mode.

Launch electra app. 

press "jailbreak".

wait for exploit to complete with blank screen.

Enter pin to unlock iphone. 

Check Electra app if iphone is "jailbroken".


## Additional Sileo repositories.

https://build.frida.re
https://coolstar.org/publicrepo/
https://repo.hackyouriphone.org

## Get Cydia

By default Sileo is the only one that will be installed by Electra. 

Using the iphone, visit download.cydiacloud.com to get "Cydia Demo".

## Get Xcode

Visit "iOS version history - Wikipedia" to find the correct xcode version for macbook.

Xcode version 10.1 from apple's old downloads ( https://developer.apple.com/downloads/more/ )

unplug the iphone and close off iTunes.

Open up xcode to ensure that it is properly installed.

Check if active developer directory is in `/Applications/Xcode.app/Contents/Developer`. It should not be `/Library...`.

Install the command line tools with `xcode-select --install`.

Check if the command line tools are working... 

if running the following command produces something like the following. This means that there are some conflicts.
```
$ xcodebuild
dyld: Library not loaded: @rpath/DVTFoundation.framework/Versions/A/DVTFoundation
  Referenced from: /Applications/Xcode.app/Contents/Developer/usr/bin/xcodebuild
  Reason: image not found
Abort trap: 6
```
try to close terminal tab and reopen a new tab.



# Get IPA from installed apps

## Get Clutch
```
git clone https://github.com/KJCracks/Clutch.git
cd Clutch
xcodebuild clean build
cd build
file Clutch
scp Clutch root@<ip of iphone>:/usr/bin/
```
ssh into iphone and call `Clutch`.

```
iPhone:~ root# Clutch
2019-07-18 15:56:00.484 Clutch[1616:41063] command: None command
Usage: Clutch [OPTIONS]
-b --binary-dump                 Only dump binary files from specified bundleID
-d --dump                        Dump specified bundleID into .ipa file
-i --print-installed             Prints installed applications
   --clean                       Clean /var/tmp/clutch directory
   --version                     Display version and exit
-? --help                        Displays this help and exit
-n --no-color                    Prints with colors disabled
-v --verbose                     Print verbose messages
```

## Find bundleID

Launch an app in iphone. Before the app closes, use `frida-ps` to capture its Identifier which is the bundleID.

```
Somes-MacBook-Pro:build user2$ frida-ps -Ua
 PID  Name             Identifier             
----  ---------------  -----------------------
1152  Mail             com.apple.mobilemail   
1634  XXXXXX           XXXXXXXX      
1559  Settings         com.apple.Preferences  
1545  Sileo            org.coolstar.SileoStore
1659  XXXXXX XXXXXXXX  XXXXXXXXX 
```
OR
```
clutch -i
```

