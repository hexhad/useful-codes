# Theme Provider - React Native
## ThemeContext.js
```
import { createContext, useContext, useEffect, useState } from "react";
import { mmkvStorage } from "../redux/persist/storage";

export const ThemeContext = createContext();

const MAIN_STATES = {
  DARK: "dark",
  LIGHT: "light",
  NAME: "theme",
};

const ThemeProvider = ({ children }) => {
  const [selectedTheme, setSelectedTheme] = useState(getInitialState);

  const getInitialState = async () => {
    try {
      const theme = await mmkvStorage.getItem(MAIN_STATES.NAME);
      setSelectedTheme(!!theme ? theme : MAIN_STATES.LIGHT);
    } catch (e) {
      setSelectedTheme(MAIN_STATES.LIGHT);
    }
  };

  useEffect(() => {
    getInitialState();
  }, []);

  const setThemeState = async (theme) => {
    await mmkvStorage.setItem(MAIN_STATES.NAME, theme ?? MAIN_STATES.LIGHT);
  };

  const toggleState = () => {
    setSelectedTheme(prevState => {
      let newState = prevState === MAIN_STATES.LIGHT ? MAIN_STATES.DARK : MAIN_STATES.LIGHT;
      setThemeState(newState);
      return newState;
    });
  };

  return (
    <ThemeContext.Provider value={{ selectedTheme, toggleState }}>
      {children}
    </ThemeContext.Provider>
  );
};

const useTheme = () => {
  const context = useContext(ThemeContext);

  if (context === undefined) {
    throw new Error("useTheme must be used within a ThemeProvider");
  }
  return context;
};

export { ThemeProvider, useTheme };
```

# Usage
## Wrapper
```
<ThemeProvider>
 ...
</ThemeProvider>
```

## state and toggleFunction
```
const { selectedTheme, toggleState } = useTheme();
```

