# 6_Inject a JavaScript bundle into HTML with the HtmlWebpackPlugin

- webpack을 사용하여 React를 호스팅된 HTML로 변환



### 설치

```bash
npm i -D html-webpack-plugin
yarn add html-webpack-plugin --dev
```



### 소스코드

##### webpack.config.js

```js
const path = require('path')
const HtmlWebpackPlugin = require('html-webpack-plugin')

module.exports = {
  mode: 'production',
  entry: './src/index.js',
  output: {
    path: path.join(__dirname, 'dist'),
    filename: 'app.bundle.js'
  },
  module: {
    rules: [
      {
        test: /\.js$/,
        loader: 'babel-loader',
        exclude: /node_modules/,
        options: {
          presets: ['@babel/preset-env', '@babel/preset-react']
        }
      }
    ]
  },
  plugins: [new HtmlWebpackPlugin()]
}
```



##### dist/index.html

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8" />
  <title>Webpack App</title>
</head>
<body>
<script type="text/javascript" src="app.bundle.js"></script>
</body>
</html>
```

- `dist/index.html`
  - HTML 파일을 가르키지만 React App은 표시 X
  - React app이 마운트되지 않음
  - HTML 템플릿을 제공해줘야함



##### src/index.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <title>React Boilerplate</title>
</head>
<body>
  <div id="app"></div>
</body>
</html>
```



##### webpack.config.js

```js
...
plugins: [new HtmlWebpackPlugin({
    template: './src/index.html'
  })]
...
```



### webpack watch mode

- 파일의 변경사항을 웹에 반영된 것을 확인하기 위해서 
  - 현재까지의 설정에서는 빌드 후 웹 페이지 새로고침을 해야 변경 사항 적용을 화긴 할 수 있음
  - watch 모드에서 webpack을 실행하면 파일을 저장할 때마다 자동으로 다시 빌드



##### package.json

```json
"scripts": {
    "build": "webpack",
    "dev": "webpack --watch --mode development",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
```

