# Fix M1 issue XCode- React Native

## Edit Pod file

### add below code after 

```
__apply_Xcode_12_5_M1_post_install_workaround(installer)

// after ^ line

installer.pods_project.targets.each do |target|
   target.build_configurations.each do |config|
      config.build_settings['IPHONEOS_DEPLOYMENT_TARGET'] = '12.4'
   end
end
```
