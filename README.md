# Extremely Basic React Boilerplate 2022 <!-- omit in toc -->

Bare bones React setup with webpack and babel

- [Initialise the package](#initialise-the-package)
- [Install Dependencies](#install-dependencies)
  - [Install React](#install-react)
  - [Install webpack](#install-webpack)
  - [Install Babel loaders](#install-babel-loaders)
  - [tldr](#tldr)
- [Create files and folders](#create-files-and-folders)
  - [Folder Structure](#folder-structure)
  - [index.html](#indexhtml)
  - [index.js](#indexjs)
  - [App.js](#appjs)
  - [webpack.config.js](#webpackconfigjs)
- [Add Scripts](#add-scripts)
- [Build](#build)
- [Start](#start)

## Initialise the package

`yarn init`

---

## Install Dependencies

### Install React

```
yarn add react react-dom
```

### Install webpack

```
yarn add -D webpack webpack-cli webpack-dev-server html-webpack-plugin
```

### Install Babel loaders

```
yarn add -D @babel/core @babel/preset-env @babel/preset-react babel-loader
```

---

### tldr

```
yarn add react react-dom

yarn add -D webpack webpack-cli webpack-dev-server html-webpack-plugin @babel/core @babel/preset-env @babel/preset-react babel-loader
```

---

## Create files and folders

### Folder Structure

```
├──src
│   ├──App.js
│   ├──index.js
│   ├──index.html
│   └──index.css
├──yarn-lock.json
├──package.json
└──webpack.config.json
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

### index.js

```js
import React from 'react'
import ReactDOM from 'react-dom'
import App from './App'

ReactDOM.render(<App />, document.getElementById('app'))
```

### App.js

```js
import React from 'react'

export default function App() {
  return <h1>Hello World</h1>
}
```

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
    ],
  },
  plugins: [
    new HtmlWebPackPlugin({
      template: './src/index.html',
    }),
  ],
}
```

---

## Add Scripts

In package.json

```json
"scripts": {
    "build": "webpack --mode production",
    "start": "webpack serve --mode development --port 9000"
  },
```

## Build

`yarn build`

output to dist folder

---

## Start

`yarn start`

http://localhost:9000
