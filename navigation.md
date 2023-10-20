## Navigation - React Native

## Run
```shell
 yarn add @react-navigation/native react-native-screens react-native-safe-area-context @react-navigation/stack react-native-gesture-handler @react-native-masked-view/masked-view @react-navigation/bottom-tabs
```
>android/app/src/main/java/<your package name>/MainActivity.java.
```javascript
import android.os.Bundle;

public class MainActivity extends ReactActivity {
  // ...
  @Override
  protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(null);
  }
  // ...
}
```
# index.js
```js
import 'react-native-gesture-handler';
```
```shell
cd ios && pod install && cd ..
```
## Constants
```js
export const SCREEN_NAMES = {
  HOME_SCREEN:'HOME_SCREEN',
  EXTRA_SCREEN:'EXTRA_SCREEN',
  SETTINGS_SCREEN:'SETTINGS_SCREEN',
  BOTTOM_NAV:'BOTTOM_NAV',
  ONBOARDING_SCREEN:'ONBOARDING_SCREEN',
}
```
## Stack
```js
import { createStackNavigator, NavigationContainer } from "@react-navigation/stack";
import BottomNavigation from "./BottomNavigation";
import { SCREEN_NAMES } from "../../utils/constants";
import OnboardingScreen from "../../screens/OnboardingScreen";

const Stack = createStackNavigator();

export default () => {
  return (
      <NavigationContainer>
         <Stack.Navigator initialRouteName={SCREEN_NAMES.ONBOARDING_SCREEN} screenOptions={{ headerShown: false }}>
             <Stack.Screen
                 name={SCREEN_NAMES.ONBOARDING_SCREEN}
                 component={OnboardingScreen}
                 options={{ headerShown: false }}
             />
             <Stack.Screen
                 name={SCREEN_NAMES.BOTTOM_NAV}
                 component={BottomNavigation}
                 options={{ headerShown: false }}
             />
         </Stack.Navigator>
    </NavigationContainer>
  );
}
```

## Bottom Navigation
```js
import { createBottomTabNavigator } from "@react-navigation/bottom-tabs";
import { Bookmark, Coffee, Hexagon } from "react-native-feather";
import { SCREEN_NAMES } from "../../utils/constants";
import HomeScreen from "../../screens/bottomNavigation/HomeScreen";
import ExtraScreen from "../../screens/bottomNavigation/ExtraScreen";
import SettingsScreen from "../../screens/bottomNavigation/SettingsScreen";

export default () => {
  const Tab = createBottomTabNavigator();
  return (
    <Tab.Navigator>
      <Tab.Screen
        name={SCREEN_NAMES.HOME_SCREEN}
        component={HomeScreen}
        options={{
          headerTitleAlign: "center",
          headerShown: true,
          tabBarShowLabel: false,
          tabBarIcon: ({ focused }) => (
            <Coffee
              stroke={focused ? "#000" : "#808080"}
              width={20}
              height={20}
            />
          ),
        }}
      />
      <Tab.Screen
        name={SCREEN_NAMES.EXTRA_SCREEN}
        component={ExtraScreen}
        options={{
          headerTitleAlign: "center",
          headerShown: true,
          tabBarShowLabel: false,
          tabBarIcon: ({ focused }) => (
            <Bookmark
              stroke={focused ? "#000" : "#808080"}
              width={20}
              height={20}
            />
          ),
        }}
      />
      <Tab.Screen
        name={SCREEN_NAMES.SETTINGS_SCREEN}
        component={SettingsScreen}
        options={{
          headerTitleAlign: "center",
          headerShown: true,
          tabBarShowLabel: false,
          tabBarIcon: ({ focused }) => (
            <Hexagon
              stroke={focused ? "#000" : "#808080"}
              width={20}
              height={20}
            />
          ),
        }}
      />

    </Tab.Navigator>
  );
}
```
