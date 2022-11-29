---
created: 1660025636879
desc: ''
id: fhk4rbi1ph2xmhf2bkqbvlt
title: React Native
updated: 1660231409681
---
   
Topics::  [programming](../topics/programming.md), [android](../devlog/android.md)   
   
   
---   
   
React Native along with [javascript.Reactjs](../devlog/javascript.Reactjs.md) you can make native mobile apps for [iOS](../devlog/iOS.md) and [Android](../devlog/android.md).   
   
   
- Reactjs is independent of React Native   
- Reactjs is a [languages.javascript](../devlog/languages.javascript.md) library for building interfaces and it's typically used for Web Development.   
- Reactjs uses React DOM library that actually adds the Web support.   
- Reactjs really is platform agnostic.   
- React Native is more comparable to React DOM than Reactjs itself.   
- React Native ships with builtin components you can use, those components are then compiled to Native UI elements for both iOS and Android.   
- It also exposes Native platform's APIs that you can use in your Javascript code.   
   
## Under the Hood   
   
You use JSX React Native components to write code in Javascript, these components are compiled to respective native elements/components. But the Javascript logic is not compiled.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1660026152/wiki/cuok3ifb3ftbyzrnueb8.png)   
   
Components are compiled to their respective native components.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1660026312/wiki/o1yfovc3cpocm4oq11le.png)   
   
Javascript logic outside of JSX is not compiled. It is actually running on a Javascript thread hosted by React Native in the native app that was built.   
   
## Getting Started (with Expo)   
   
   
- Install Nodejs   
- Install Expo cli   
- Init Expo project   
  - `expo init projectName`   
   
## Debugging   
   
   
- Read **Warning** messages in Consoles.   
- Follow the Stacktrace for the file/components that's causing the error.   
- Read the documentation and understand how the props of a certain component works.   
- For additional insights use `console.log()` messages in your application.   
- **Debugging Javascript remotely**   
  - Press `m` in console to open menu on your emulator(or `Ctrl` + `m`).   
  - Toggle "Debug Remote JS" to open up Chrome Developer Tools in a new browser window.   
- **React DevTools** - install this Globally or as a Dev Dependency.   
  - `npm install -g react-devtools`   
  - `react-devtools`   
  - Toggle `Debug Remote JS` from Expo menu.   
  - Explore the components tree, mess around with your components, props, state.   
   
## DevTools   
   
## Project   
   
   
- [javascript.react native goals app](../devlog/javascript.react%20native%20goals%20app.md)