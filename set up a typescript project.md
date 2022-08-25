## Look through tutorial on youtube with ben awad

https://www.youtube.com/watch?v=1UcLoOD1lRM&t=1018s

Give package.json
npm init -y

Add typescript as a dev dependancies
yarn add -D typescipt

tsc is the typescript compiler is also creates you tsconfig file
npx tsc --init

To compile before running:

"scripts":
  "build": "tsc"
  
yarn build
  
this allows to compile ts files back to javascript

then run it with node

node src/index.js

yarn add -D ts-node

in package.json

scripts
  "start": "ts-node <file>"
  
yarn start

If want to track changes

yarn add -D ts-node-dev


scripts
  "start": "ts-node-dev --respawn <file>"
  
yarn add -D nodemon

scripts
  "start": "ts-node-dev --respawn <file>"
  "dev": "nodemon --exec ts-node src/index.ts"
  
yarn add express

we need to add typescript defintions
yarn add -D @types/node
yarn add -D @types/express

For when you do not have the types for the packages
folder @types
  create file <name>.d.ts
    declare module <name>
    
Look if you may need to restart the server    

You can get around typescipt type checking:

(req as any).name = "bob"

Undefined

add (a, b) => {
  return a + b
}
Will throw an error with type

you can make a param optional by putting a question mark afterward
doSometing (a?: number)
when you want to make something undefined

a + b!

you can also to the following to ignore tscode
// @ts-ignore

// for passing in objects
interface Params{
  a: number
  b: number
}

// for everything else
type Add = (a: number, b: number) => void

const add: Add = (x: Params) => {
  return x.a + x.b
}
