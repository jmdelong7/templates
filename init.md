# Start

Make new repo in github, copy [SSH link], be in repos folder in terminal

git clone [SSH link] && cd [repo name]

mkdir src && cd src && touch index.html index.js styles.css && cd ..
touch webpack.common.js webpack.dev.js webpack.prod.js .gitignore

npm init -y
npm install --save-dev webpack webpack-cli webpack-dev-server
npm install --save-dev webpack-merge
npm install --save-dev html-webpack-plugin
npm install --save-dev html-loader
npm install --save-dev style-loader css-loader

Add the following to scripts section then save and close:
"dev": "webpack serve --open --config webpack.dev.js",
"build": "webpack --config webpack.prod.js",
"deploy": "git subtree push --prefix dist origin gh-pages"

# .gitignore

#Node modules
node_modules/

#Build output directory
dist/
build/

#Development server
.webpack/

#Environment variables
.env
.env.local
.env.\*

#Cache directories
.cache/
.npm/

#IDE specific files
.vscode/
.idea/
_.swp
_.swo

#OS generated files
.DS_Store
Thumbs.db

# webpack.common.js

const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');

module.exports = {
  entry: {
    app: './src/index.js',
  },
  plugins: [
    new HtmlWebpackPlugin({
      template: './src/index.html',
    }),
  ],
  output: {
    filename: '[name].bundle.js',
    path: path.resolve(__dirname, 'dist'),
    clean: true,
  },
  module: {
    rules: [
      {
        test: /\.css$/i,
        use: ['style-loader', 'css-loader'],
      },
      {
        test: /\.(woff|woff2|eot|ttf|otf)$/i,
        type: 'asset/resource',
        generator: {
          filename: 'fonts/[name][ext]'
        }
      },
      {
        test: /\.html$/i,
        loader: "html-loader",
      }      
    ],
  },
};

# webpack.dev.js

const { merge } = require('webpack-merge');
const common = require('./webpack.common');

module.exports = merge(common, {
  mode: 'development',
  devtool: 'inline-source-map',
  devServer: {
    static: './dist',
    watchFiles: ['src/**/*'],
    open: true,
    hot: true,
  },
});

# webpack.prod.js

const { merge } = require('webpack-merge');
const common = require('./webpack.common');

module.exports = merge(common, {
  mode: 'production',
  output: {
    publicPath: '/coordinator-tools/',  // Add this line - must match your repo name
  }
});
