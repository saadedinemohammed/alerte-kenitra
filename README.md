Zurich Mobile App
=================

A mobile app for www.zueriwieneu.ch based on mSociety's FixMyStreet platform.

Setup
-----
This project uses Apache Cordova to produce Android and iOS apps. There is
some mildly complicated configuration and setup required to be able to develop
with it. The following all assumes you're working on a Mac.

1. Make sure you have the latest versions of XCode, the Android SDK, node and
npm installed. It's a very good idea to have installed the Intel HAXM versions
of the Android emulator because they're about 100 times faster to run. You need
to download it from the Android SDK Manager (run `android` on the command line)
and then actually run the `.dmg` that this creates in your sdk folder.

2. Install the cordova CLI with npm: `npm install -g cordova`
Note that this is not the same as the phonegap CLI and the two should not be
mixed up. The latter gives you access to Adobe's proprietary phonegap build
service, which we **don't** use!

3. Checkout the project

4. `cd` into the project directory and install the Cordova platforms you need:
`cordova platform add android` and `cordova platform add ios`

5. Add the cordova plugins we use. As of writing the list is: (from `cordova plugin list`)

   ```
   org.apache.cordova.battery-status 0.2.11 "Battery"
   org.apache.cordova.camera 0.3.2 "Camera"
   org.apache.cordova.contacts 0.2.13 "Contacts"
   org.apache.cordova.device 0.2.12 "Device"
   org.apache.cordova.device-motion 0.2.10 "Device Motion"
   org.apache.cordova.device-orientation 0.3.9 "Device Orientation"
   org.apache.cordova.dialogs 0.2.10 "Notification"
   org.apache.cordova.file 1.3.1 "File"
   org.apache.cordova.file-transfer 0.4.6 "File Transfer"
   org.apache.cordova.geolocation 0.3.10 "Geolocation"
   org.apache.cordova.globalization 0.3.1 "Globalization"
   org.apache.cordova.media 0.2.13 "Media"
   org.apache.cordova.media-capture 0.3.3 "Capture"
   org.apache.cordova.network-information 0.2.12 "Network Information"
   org.apache.cordova.splashscreen 0.3.3 "Splashscreen"
   ```

   So to install them: `cordova plugin install org.apache.cordova.battery-status org.apache.cordova.camera org.apache.cordova.contacts org.apache.cordova.device org.apache.cordova.device-motion org.apache.cordova.device-orientation org.apache.cordova.dialogs org.apache.cordova.file org.apache.cordova.file-transfer org.apache.cordova.geolocation org.apache.cordova.globalization org.apache.cordova.media org.apache.cordova.media-capture org.apache.cordova.network-information org.apache.cordova.splashscreen`

   (These might be installed automatically, I'm not totally sure how Cordova remembers them)

6. Copy `www/js/config.js-example to www/js/config.js` and edit if needed

7. To run the project on one of the platforms, use: `cordova emulate ios` or `cordova emulate android`
(You might need to `npm install -g ios-sim` to run it on ios)

Tips and Tricks
--------------
- Make sure you read the documentation for Cordova from http://cordova.apache.org/
**not the Phonegap site** - the two vary in infuriating and subtle ways and much
of the stackoverflow-esque info on the web is confused about which one it's for.
Particularly in the options for things in `config.xml` which is where all the
magic happens.
- You can use `ios-sim` to launch the iOS emulator directly with something like:
`ios-sim launch platforms/ios/build/emulator/Zuri\ Wie\ Neu.app --devicetypeid "com.apple.CoreSimulator.SimDeviceType.iPhone-6, 8.0"` after you've built the project via a previous
emulator run or a direct build via `cordova build ios`. This allows you to
specify a different device than the default one. To see the available options
for `--devicetypeid` run `ios-sim showdevicetypes`.
- You can open the iOS project in XCode if you prefer to run it that way, the
project file is in `platforms/ios`
- The `platforms`, `plugins` and `hooks` folders are auto-generated by Cordova
no need to check them in (hence why they're .gitignored), you should only need
to check in the `www` folder and `config.xml`, plus possibly `/merges` if you
ever use that functionality.
- To check the console log output when emulating iOS, run: `tail -f console.log`
Cordova by default writes it out to that file in your project root
- To check the console log output when emulating Android, cd to
`platforms/android/cordova` and run `./log`. I found that I needed to be in the
directory for it to actually print anything, YMMV.
- Leave the emulators running once they start, it's much quicker!