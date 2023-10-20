## Navigation - React Native

## Run
```
yarn add 
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
import { createStackNavigator } from "@react-navigation/stack";
import BottomNavigation from "./BottomNavigation";
import { SCREEN_NAMES } from "../../utils/constants";
import OnboardingScreen from "../../screens/OnboardingScreen";

const Stack = createStackNavigator();

export default () => {
  return (
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
