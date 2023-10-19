# Compress Images - React Native

## Run
```
yarn add react-native-compressor react-native-fs react-native-image-crop-picker
```

## Code
```
const onPressImageSetup = async () => {
    // const options = {
    //   mediaType: 'photo',
    //   includeBase64: false,
    //   maxHeight: 2000,
    //   maxWidth: 2000,
    // };

    // let response = await launchImageLibrary(options);
    // if (response.didCancel) {
    //   console.log('User cancelled image picker');
    // } else if (response?.error) {
    //   console.log('Image picker error: ', response.error);
    // } else {
    //   let imageUri = response?.uri || response.assets?.[0]?.uri;
    //   console.log('imageUri',imageUri);
    //
    //   let imageCompressed =  await Image.compress(imageUri);
    //   console.log('compress',imageCompressed);
    // }

    let ImagePickerTest = await ImagePicker.openPicker({
        multiple: true,
        maxFiles: 10,
        waitAnimationEnd: false,
        includeExif: true,
        forceJpg: true,
        mediaType: "photo",
        compressImageQuality: 0.2,
    })

    let imageUri = ImagePickerTest[0]?.sourceURL;
    let imageCompressed =  await Image.compress(imageUri);

    const originalFileSize = await fileSize(imageUri);
    const compressedFileSize = await fileSize(imageCompressed);

    console.log('original','path',imageUri.substring(imageUri?.length-20));
    console.log('compressed','path',imageCompressed.substring(imageCompressed?.length-20));
    console.log('original','size',originalFileSize?.size/1000000,'MB');
    console.log('compressed','size',compressedFileSize?.size/1000000,'MB');

};
  
const fileSize = async (path) => await RNFS.stat(path)
```
