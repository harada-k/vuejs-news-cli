# vuejs-news

## about
forkしてきた以下のリポジトリを、Vue CLIを使って作り直してみた。  
https://github.com/harada-k/vuejs-news

## やってみたこと
- fork元を参考に、NYTimesのAPIから、Vue.js、Axiosを使用して記事情報を取得する
- Vue CLIを使用し、単一ファイルコンポーネントで構成するように変更
- 記事カセットは、`css grid`を使ってレイアウトするように変更
    - 元はレイアウトのために4データごとに区切っていたが、その必要がなくなった
- `select`メニューの変更をトリガーにして、記事カセットを表示するように変更

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Run your tests
```
npm run test
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
