# TODO Custom Hook - React Native

## Hook
```js
import { useState } from "react";

export const useArrayState = (initialState = []) => {
  const [state, setState] = useState(initialState);

  const add = (newValue) => {
    setState(prevState => [...prevState, newValue]);
  };

  const remove = (index) => {
    setState(prevState => {
      const tempState = [...prevState];
      tempState.splice(index, 1);
      return tempState;
    });
  };

  const update = (index,value) => {
    setState(prevState => {
      const tempState = prevState?.map((item,i)=>{
        if (index===i){
          return {value};
        } else {
          return item;
        }
      });
      return tempState;
    });
  }

  return [state, { add, remove, update }];
};
```

## Usage
```js
import { FlatList, SafeAreaView, Text, TouchableOpacity, View } from "react-native";
import { useArrayState } from "./customHooks";

export default () => {
    const [state, { add, remove, update }] = useArrayState([]);
    return (
        <SafeAreaView>
            <TouchableOpacity onPress={() => {
                add({ value: "lorem" });
            }}>
                <Text>Add</Text>
            </TouchableOpacity>
            <FlatList data={state} renderItem={({ item, index }) => {
                return (
                    <View>
                        <Text>{item?.value}</Text>
                        <TouchableOpacity onPress={() => remove(index)}>
                            <Text>DELETE</Text>
                        </TouchableOpacity>
                        <TouchableOpacity onPress={() => update(index, "UPDATED")}>
                            <Text>UPDATE</Text>
                        </TouchableOpacity>
                    </View>
                );
            }} />
        </SafeAreaView>
    );
}
```
