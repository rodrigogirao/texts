# Create a scrapper lib for tracking Brazilian package

## Configure project

### First we have to crate a new typescript project:

```sh
$ yarn init
yarn init v1.22.5
question name: track-pack-correios-lib
question version (1.0.0):
question description: A scrapper package to get packaging tracking from Brazilian post offices (correios)
question entry point: src/index.ts
question repository url: git@github.com:rodrigogirao/track-pack-correios-lib.git
question author: Rodrigo Girão
question license (MIT):
question private:
success Saved package.json
✨  Done in 227.98s.
```

### Add dependencies (-D is for devDependencies):

```sh
$ yarn add @types/node typescript
$ yarn add -D ts-node
```

### Init a typescript project by creating a `tsconfig.json`, to compile Typescript to Javascript

```sh
$ yarn tsc --init --rootDir src --outDir dist
```

### Create your root file in `src` folder:

```sh
$ mkdir src
$ echo "console.log('Hello World from Brazil!')" > src/index.ts
```

### Compile the project:

```sh
$ yarn tsc
```

Notice that when you run the command above a new file `index.js` was created in the `dist` folder, now we can run it:

```sh
$ node dist/index.js
Hello World from Brazil!
```

To run the project without keep compile it every time we can use `ts-node` to do it on the fly:

```sh
$ yarn ts-node src/index.ts
```

Now that we have these 3 command we can add some aliases to them. Add the following above `"dependencies"` in the package.json

```json
  "scripts": {
    "build": "tsc",
    "start": "node dist/index.js",
    "dev": "ts-node src/index.ts"
  },
```

```sh
$ yarn build

yarn run v1.22.5
$ tsc
✨  Done in 1.42s.
```

```sh
yarn start
yarn run v1.22.5
$ node dist/index.js
Hello World from Brazil!
✨  Done in 0.14s.
```

```sh
yarn dev
yarn run v1.22.5
$ ts-node src/index.ts
Hello World from Brazil!
✨  Done in 1.71s.
```

Add `nodemon` dependency to restart the application when the files changed

```sh
$ yarn add -D nodemon
```

Let's change the `dev` script in `package.json` to add `nodemon`

```json
"scripts": {
  // ...other scripts
    "dev": "nodemon --watch 'src/**/*.ts' --exec 'ts-node' src/index.ts"
  },
```

Run to see what happens:

```sh
$ yarn dev
```

**yarn run v1.22.5**  
<span style="color:darkgray">**$ nodemon --watch 'src/\*\*/\*.ts' --exec 'ts-node' src/index.ts**</span>  
<span style="color:yellow">**[nodemon] 2.0.7**</span>  
<span style="color:yellow">**[nodemon] to restart at any time, enter \`rs\`**</span>  
<span style="color:yellow">**[nodemon] watching path(s): src/\*\*/\*.ts**</span>  
<span style="color:green">**[nodemon] watching extensions: ts,json**</span>  
<span style="color:green">**[nodemon] starting \`ts-node src/index.ts`**</span>  
Hello World from Brazil!  
<span style="color:green">**[nodemon] clean exit - waiting for changes before restart**</span>

As we can see above now every time a file is change the nodemon will restart automatically

### Adding dependencies for scraper

```sh
yarn add axios cheerio
yarn add -D @types/axios @types/cheerio
```

## Build the scraper

### Creating api calls structure

> Links:  
> https://classic.yarnpkg.com/en/docs/cli/init/ https://classic.yarnpkg.com/en/docs/cli/add  
> https://www.typescriptlang.org/docs/handbook/tsconfig-json.html  
> https://github.com/TypeStrong/ts-node  
> https://dev.to/caelinsutch/building-a-web-scraper-in-typescript-14l1
