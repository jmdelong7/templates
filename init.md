# Start

Make new repo in github, copy [SSH link], be in repos folder in terminal.

git clone [SSH link] && cd [repo name].

mkdir src && cd src && touch index.html index.js styles.css && cd ..
mkdir webpack && cd webpack
touch webpack.common.js webpack.dev.js webpack.prod.js && cd ..
touch .gitignore .env

npm init -y
npm install --save-dev webpack webpack-cli webpack-dev-server
npm install --save-dev webpack-merge
npm install --save-dev html-webpack-plugin
npm install --save-dev html-loader
npm install --save-dev style-loader css-loader
npm install --save-dev babel-jest @babel/core @babel/preset-env

Used for saving keys in a .env file. Can be accessed with process.env.KEY
npm install --save-dev dotenv-webpack

Used for deploying to github pages with easy deploy command.
npm install --save-dev gh-pages
