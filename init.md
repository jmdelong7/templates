# Start

Make new repo in github, copy [SSH link], be in repos folder in terminal

git clone [SSH link] && cd [repo name]

mkdir src && cd src && touch index.html index.js styles.css && cd ..
touch webpack.common.js webpack.dev.js webpack.prod.js .eslint.config.mjs .gitignore

npm init -y
npm install --save-dev webpack webpack-cli webpack-dev-server
npm install --save-dev webpack-merge
npm install --save-dev html-webpack-plugin
npm install --save-dev style-loader css-loader

npm init @eslint/config@latest
Won't work if there are multiple projects open using eslint.

Add the following to scripts section then save and close:
  "lint": "eslint .",
  "dev": "webpack serve --open --config webpack.dev.js",
  "build": "webpack --config webpack.prod.js",
  "deploy": "git subtree push --prefix dist origin gh-pages"

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
    publicPath: '/form-validation/',  // Add this line - must match your repo name
  }
});




