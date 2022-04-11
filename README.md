# Extremely Basic React Boilerplate 2022 <!-- omit in toc -->

Bare bones React setup with webpack and babel

![hello](docs/images/hello-world.png)

- [Initialise the package](#initialise-the-package)
- [Install Dependencies](#install-dependencies)
  - [Install React](#install-react)
  - [Install webpack](#install-webpack)
    - [What even is webpack?](#what-even-is-webpack)
  - [Install Babel loaders](#install-babel-loaders)
  - [tldr](#tldr)
- [Create files and folders](#create-files-and-folders)
  - [index.html](#indexhtml)
  - [index.js](#indexjs)
  - [App.js](#appjs)
  - [index.css](#indexcss)
  - [webpack.config.js](#webpackconfigjs)
    - [What is this doing?](#what-is-this-doing)
- [Add Scripts](#add-scripts)
- [Build](#build)
- [Start](#start)
- [References](#references)

---

## Initialise the package

`yarn init`

---

## Install Dependencies

### Install React

- react — main react library
- react-dom — allows us to use react in the browser

```
yarn add react react-dom
```

---

### Install webpack

- webpack — JavaScript bundler
- webpack-cli — run webpack commands from the command line.
- webpack-dev-server - allows us to run the site on localhost
- html-webpack-plugin - adds the bundled js file into the html

```
yarn add -D webpack webpack-cli webpack-dev-server html-webpack-plugin
```

---

#### What even is webpack?

webpack is a JavaScript code bundler that traverses the dependency graph of your project (chain of imports you use in your JS files), and creates a static JavaScript file(s) that is ready to be attached to your HTML.

- Entry — This is the top of the dependency tree (conventionally and default src/index.js) where webpack starts with the bundling process.
- Output — The output file(s). AKA the bundle.
- Loaders — webpack, by default, only works with JavaScript files, but we obviously want to be able to import other file types(CSS, JSX, etc.). This is where loaders come into play. They are packages (not included with Webpack itself) that help us import non-JavaScript files directly into our JavaScript.
- Plugins — Plugins are also other third party packages that can be used with webpack to extend it’s functionality. e.g html-webpack-plugin.

---

### Install Babel loaders

- @babel/core - Babel itself
- @babel/preset-env - preset for compiling ES2015+ syntax
- @babel/preset-react - preset that allows us to work with React/jsx
- babel-loader - loads the files (in this case jsx)
- style-loader
- css-loader

```
yarn add -D @babel/core @babel/preset-env @babel/preset-react babel-loader style-loader css-loader
```

---

### tldr

```
yarn add react react-dom

yarn add -D webpack webpack-cli webpack-dev-server html-webpack-plugin @babel/core @babel/preset-env @babel/preset-react babel-loader style-loader css-loader
```

---

## Create files and folders

Here is the folder structure

```
├──src
│   ├──App.js
│   ├──index.js
│   ├──index.html
│   └──index.css
├──webpack.config.json
├──package.json
└──yarn-lock.json
```

---

### index.html

```html
<!DOCTYPE html>
<html>
  <head>
    <title>React with Webpack - Basic Boilerplate</title>
  </head>
  <body>
    <div id="app"></div>
    <script src="../dist/main.js"></script>
  </body>
</html>
```

---

### index.js

```js
import React from 'react'
import ReactDOM from 'react-dom'
import App from './App'

ReactDOM.render(<App />, document.getElementById('app'))
```

---

### App.js

```js
import React from 'react'

import './index.css'

export default function App() {
  return <h1>Hello World</h1>
}
```

---

### index.css

Basic example just for illustration

```css
body {
  font-family: 'Courier New', Courier, monospace;
}
```

---

### webpack.config.js

```js
const path = require('path')
const HtmlWebPackPlugin = require('html-webpack-plugin')

module.exports = {
  entry: '/src/index.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
  },
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        exclude: /node_modules/,
        use: {
          loader: 'babel-loader',
          options: {
            presets: ['@babel/preset-env', '@babel/preset-react'],
          },
        },
      },
      {
        test: /\.css$/,
        exclude: /node_modules/,
        use: [{ loader: 'style-loader' }, { loader: 'css-loader' }],
      },
    ],
  },
  plugins: [
    new HtmlWebPackPlugin({
      template: './src/index.html',
    }),
  ],
}
```

#### What is this doing?

- entry - setting the entry js file to start traversing the dependency tree from
- output - where to save the bundled files
- module.rules - e.g. use babel-loader, whenever it sees any file ending in either js or jsx. Use style loader then css loader when loading css files
- plugins - `HtmlWebPackPlugin` - add/update the script path in the html to be the bundled js file and copy to the output folder

---

## Add Scripts

In package.json

```json
"scripts": {
    "build": "webpack --mode production",
    "start": "webpack serve --mode development --port 9000"
  },
```

---

## Build

`yarn build`

output to dist folder

---

## Start

`yarn start`

http://localhost:9000

---

## References

- Very useful write up that I borrowed heavily from here - all credit to them for much of the info summarising webpack and babel - [https://levelup.gitconnected.com/how-to-setup-a-react-application-with-webpack-f781b5c4a4ab](https://levelup.gitconnected.com/how-to-setup-a-react-application-with-webpack-f781b5c4a4ab)
