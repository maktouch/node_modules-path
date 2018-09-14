

Get the path of the `node_modules` folder in your scripts or CLI or `package.json`. This is useful when you are building a library that can either be used as an npm dependency or directly, [see this question on SO](https://stackoverflow.com/questions/44279838/copy-assets-from-npm).

You can add a parameter in order to look for a specific module. This is useful when npm creates [multiple node_modules folder for conflicts reasons](https://docs.npmjs.com/files/folders#cycles-conflicts-and-folder-parsimony).

Installation
```
npm install node_modules-path --save
```

## Access node_modules in package.json

Use it in your `packge.json` like this:

```json
"name": "my-super-project",
"scripts": {
  "build": "cp -R `node_modules`/font-awesome/fonts/* dist/fonts/",
```

With a specific module name as a param:

```json
"scripts": {
  "test": "echo  `node_modules` can differ from `node_modules module1`",
```

## node_modules folder path from another nodejs script

```
const node_modules = require('node_modules-path');
console.log('node module path for this project:', node_modules());
```

This is especially useful to serve fonts in an express app

```js
app.use('/fonts', express.static(Path.resolve(node_modules(), 'font-awesome/fonts/')));

```

With a specific module name as a param, which is safer:


```js
app.use('/fonts', express.static(Path.resolve(node_modules('font-awesome'), 'font-awesome/fonts/')));
```
