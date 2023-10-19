# Inject to WebView - React Native

```
const ref = useRef();

const run = `document.body.style.backgroundColor = 'blue'; true;`;

<WebView
  javaScriptEnabled={true}
  ref={ref}
  source={{
     uri: 'hashan.com',
  }}
  onLoad={()=>{
     ref?.current?.injectJavaScript(run)
  }}
/>
```
