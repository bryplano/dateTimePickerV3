## Purpose

This application was built with the intent of reproducing an Ionic v3 issue where the `picker` displayed by `ion-datetime` does not inherit the provided `mode` attribute on the `datetime` component.

The issue occurs on both iOS and Android. For this repo, I'm providing reproduction steps for iOS.

## Reproducing the Issue (iOS)

**These steps assume the following:**
- You have Xcode 9 or 10 installed
- You have an Apple Developer account installed & configured for running Ionic applications locally (note: you may need to change your provisioning profile / code signing in Xcode when running the app locally)
- You have the Ionic CLI & npm/NodeJS installed
- You have Safari's Developer Tools enabled

1. Download this project as a ZIP export & unzip to a local directory
2. Open Terminal and navigate to the dir
3. Run `npm i`
4. Run `ionic cordova platform add ios`
5. The next step depends on the version of Xcode you're using.

5a. If Xcode 9 is installed, run:
```
ionic cordova run ios
```
5b. If Xcode 10 is installed, run: 
```
ionic cordova run ios -- --buildFlag="-UseModernBuildSystem=0"
``` 

6. When the simulator is running, open Safari on your local machine
7. Navigate to the simulator in Safari's *Develop* menu and open localhost
8. Inspect the DOM and search for the `datetime` component - notice it is properly denoted with the `md` attribute
9. Now click or tap on the input (`datetime`) field to bring up the `picker`
10. Inspect the DOM again for the `picker` component; note that it does _not_ inherit the same `md` attribute (`picker-ios`)

## Notes
- This occurs on both devices and simulators (only tested on iOS 12+)
- This does *not* occur for an Ionic 4 application (only v3)
