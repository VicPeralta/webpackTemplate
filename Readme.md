
# Guide to install Webpack

1.- Init node  
`npm init -y`


2.- Install Webpack and webpack-cli  
`npm install webpack webpack-cli --save-dev`

3.- Create webpack.config.js  
```
const path = require('path'); 
module.exports = {  
  entry: './src/index.js',  
  output: {  
    filename: 'main.js',  
    path: path.resolve(__dirname, 'dist'),  
  },
};
```
4.- Install HtmlWebpackPlugin and adjust webpack.config.js

`npm install --save-dev html-webpack-plugin`  

```
const HtmlWebpackPlugin = require('html-webpack-plugin');

 module.exports = {
  plugins: [
    new HtmlWebpackPlugin({
      // This line is optional
      title: 'Output Management', 
      template: './src/index.html'
    }),
  ],
 };
```
5.- Cleaning up the /dist folder
```
  // Add this line to output section in order to delete
  // what the dist folder contains
  clean: true,

```
6.- Add CSS  
`npm install --save-dev style-loader css-loader`
> Add these lines to webpack.config.js
```
 module: {
    rules: [
      {
        test: /\.css$/i,
        use: ['style-loader', 'css-loader'],
      },
    ],
  },
````
>In your main script import the css file   
`import './style.css';`

7.- Loading images
>Add these lines to the module section of webpack.config.js
```
{
  test: /\.(png|svg|jpg|jpeg|gif)$/i,
  type: 'asset/resource',
},
```
What this does, is that whenever your src code reference an image, it is going to change the path in the dist folder.
So if you use ./assets/image.png, you use that path in your source code, and webpack will change that to the correct path

8.- Setup local dev server  
`npm install --save-dev webpack-dev-server`  

Change your configuration file to tell the dev server where to look for files:
```
// Within module.exports
devServer: {
    static: './dist',
  },
```
9.- Add scripts to package file

```
scripts": {
     "test": "echo \"Error: no test specified\" && exit 1",
     "watch": "webpack --watch",
    "start": "webpack serve --open",
     "build": "webpack"
   },
````