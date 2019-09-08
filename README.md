## Let's install React.js and React DOM:

npm i react react-dom --save-dev

##install Babel & Webpack
##babel-core: babel transpile ES6 code to ES5
##babel-loader: This is a webpack helper which allows to transpile Javascript files with babel and webpack. It uses babel under the hood
##babel/preset-env: It determines which features needs to be transformed to run within different browsers or runtime versions. This is also known as browser polyfills
##babel/preset-react: It is used to transform all your React JSX into functions.

 npm i @babel/core babel-loader @babel/preset-env @babel/preset-react --save-dev


 npm i webpack webpack-cli --save-dev


 #touch webpack.config.js

 module.exports = {
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        exclude: /node_modules/,
        use: {
          loader: "babel-loader"
        }
      } 
    ]
  }
};

##Install webpack-dev-server
##webpack-dev-server: Webpack has its own server called webpack-dev-server(WDS) which removes the pain of manually refreshing the browser once the changes have been saved.

npm i webpack-dev-server --save-dev
##Now add below lines inside the package.json file

"scripts": {
    "start": "webpack-dev-server --open --hot --mode development",
    "build": "webpack --mode production"
 }

 #— open: This will open the default browser and load the localhost environment running your app in the browser
#— hot: It will watch all your changes, and reload the browser automatically
#— mode: This can be development or production

#index.js

import React from "react";
import ReactDOM from "react-dom";

const App = () => {
  return <div>Hello React,Webpack 4 & Babel 7!</div>;
};

ReactDOM.render(<App />, document.querySelector("#root"));

#index.html

<!DOCTYPE html>
<!--[if lt IE 7]>      <html class="no-js lt-ie9 lt-ie8 lt-ie7"> <![endif]-->
<!--[if IE 7]>         <html class="no-js lt-ie9 lt-ie8"> <![endif]-->
<!--[if IE 8]>         <html class="no-js lt-ie9"> <![endif]-->
<!--[if gt IE 8]><!--> <html class="no-js"> <!--<![endif]-->
    <head>
        <meta charset="utf-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <title>React Webpack</title>
        <meta name="description" content="">
        <meta name="viewport" content="width=device-width, initial-scale=1">
    </head>
    <body>
        <section id="root"></section>
    </body>
</html>


##Install another webpack helper, css-loader and style-loader to make CSS work in our application. We will be importing CSS files into our components.

npm i css-loader style-loader --save-dev
##Check index.html file for the same!

##Create a .babelrc file inside the root of your project folder and insert below lines to it.
##.babelrc: As we know that, we are using babel-loader, it will look for a .babelrc file while the project is initialized
##touch .babelrc
{ 
        "presets": ["@babel/preset-env", "@babel/preset-react"]
 }

##Install HTML web pack plugin and HTML loader for displaying our page

##htmlWebPackPlugin: This generates the HTML dynamically, with an <script> tag including our bundled js file.

npm i html-webpack-plugin html-loader --save-dev

const HtmlWebPackPlugin = require("html-webpack-plugin");
module.exports = {
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        exclude: /node_modules/,
        use: {
          loader: "babel-loader"
        }
      },
      {
        test: /\.html$/,
        use: [
          {
            loader: "html-loader"
          }
        ]
      }
    ]
  },
  plugins: [
    new HtmlWebPackPlugin({
      template: "./src/index.html",
      filename: "./index.html"
    })
  ]
};


## package.json looks like :

{
  "name": "react_web",
  "version": "1.0.0",
  "description": "",
  "main": "webpack.config.js",
  "scripts": {
    "start": "webpack-dev-server --open --hot --mode development",
    "build": "webpack --mode production"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "@babel/core": "^7.4.0",
    "@babel/preset-env": "^7.4.2",
    "@babel/preset-react": "^7.0.0",
    "babel-loader": "^8.0.5",
    "css-loader": "^2.1.1",
    "html-loader": "^0.5.5",
    "html-webpack-plugin": "^3.2.0",
    "react": "^16.8.5",
    "react-dom": "^16.8.5",
    "style-loader": "^0.23.1",
    "webpack": "^4.29.6",
    "webpack-cli": "^3.3.0",
    "webpack-dev-server": "^3.2.1"
  }
}

npm start 

##To make the build, run
npm build
