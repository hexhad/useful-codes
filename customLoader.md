# Custom Loader - React Native

## ScreenFreezer.js
```js
import { ActivityIndicator, Modal, StyleSheet, View } from "react-native";
import React from "react";

export default ({ visible }) => {
    return (
        <Modal visible={visible} transparent={true}>
            <View style={styles.container}>
                <ActivityIndicator size="large" color="#fff" style={styles.indicator} />
            </View>
        </Modal>
    );
};

const styles = StyleSheet.create({
    container: {
        flex: 1,
        opacity: 0.3,
        backgroundColor: "#000000",
        justifyContent:'center',
        alignItems:'center'
    },
    indicator: {
        flex: 1
    },
});
```

## Usage
```js
<ScreenFreezer visible={ visibilityState }/>
```
