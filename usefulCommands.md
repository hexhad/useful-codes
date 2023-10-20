# Useful Commands - React Native

## Open Xcode
```shell
xed ios/
```
## Open Android Studio
```shell
studio android/
```
## Open Emulator 
```shell
emulator -avd Pixel_4a_API_33 -no-snapshot -no-snapshot-save
```
#### adb reverse is a command that allows you to expose a port on your Android device to a port on your computer.
#### In the example above you are going to expose tcp port 8081 on the phone via port 8081 on your computer.
```shell
adb reverse tcp:8081  tcp:8081 
```
