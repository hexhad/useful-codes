Props Types - React Native

## Run
```shell
yarn add prop-types
```
## Sample Code

```js
import { Text, View } from "react-native";
import PropTypes from "prop-types";

 const Dummy = ({ dummyInteger, dummyString }) => {
  return (
    <View>
      <Text>{dummyInteger}</Text>
      <Text>{dummyString}</Text>
    </View>
  );
}

Dummy.propTypes = {
  dummyString: PropTypes.string.isRequired,
  dummyInteger: PropTypes.number.isRequired,
};

export default Dummy;
```
## Usage
```js
<Dummy dummyInteger={1} dummyString={'dummyString'}/>
```
