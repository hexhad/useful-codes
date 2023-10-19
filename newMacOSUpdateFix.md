## New MacOs Update XCode - React Native

```
post_install do |installer|
   installer.pods_project.targets.each do |target|
          target.build_configurations.each do |config|
            config.build_settings['GCC_PREPROCESSOR_DEFINITIONS'] ||= ['$(inherited)', '_LIBCPP_ENABLE_CXX17_REMOVED_UNARY_BINARY_FUNCTION']
          end
        end
    react_native_post_install(installer)
    __apply_Xcode_12_5_M1_post_install_workaround(installer)
    installer.pods_project.targets.each do |target|
    target.build_configurations.each do |config|
    config.build_settings['IPHONEOS_DEPLOYMENT_TARGET'] = '12.4'
    end
     end
    installer.pods_project.build_configurations.each do |config|
      config.build_settings["EXCLUDED_ARCHS[sdk=iphonesimulator*]"] = "arm64"
    end
  end
end
```
