# angular2-quickstart
This repo contain the Running Angular2 quick start app anf its instruction how to create angular 2 app.

Angular 2 is in TypeScript

For creating angular 2 project app we need to setup our development environment:
	
	- install node and npm
  	- create and application project folder
  	- add a tsconfig.json to guide TypeScript Compiler
  	- add a typings.json that identifies missing  TypeScript definition files
  	- add a package.json that defines the packages and scripts we need
  	- install the npm packages and typings files

**Install** [node and npm] if not already on your machine.

Create a **new project folder**

```sh
mkdir your_project_name
cd your_project_name
```

Add a `tsconfig.json` file to the project folder and copy/paste the following:

```sh
{
  "compilerOptions": {
    "target": "es5",
    "module": "system",
    "moduleResolution": "node",
    "sourceMap": true,
    "emitDecoratorMetadata": true,
    "experimentalDecorators": true,
    "removeComments": false,
    "noImplicitAny": false
  },
  "exclude": [
    "node_modules",
    "typings/main",
    "typings/main.d.ts"
  ]
}
```
This `tsconfig.json` file guides the TypeScript compiler.

Add a `typings.json` file to the project folder and copy/paste the following:

```sh
{
  "ambientDependencies": {
    "es6-shim": "github:DefinitelyTyped/DefinitelyTyped/es6-shim/es6-shim.d.ts#7de6c3dd94feaeb21f20054b9f30d5dabc5efabd",
    "jasmine": "github:DefinitelyTyped/DefinitelyTyped/jasmine/jasmine.d.ts#7de6c3dd94feaeb21f20054b9f30d5dabc5efabd"
  }
}
```

Add a `package.json` file to the project folder and copy/paste the following:

```sh
{
  "name": "angular2-quickstart",
  "version": "1.0.0",
  "scripts": {
    "start": "tsc && concurrently \"npm run tsc:w\" \"npm run lite\" ",    
    "tsc": "tsc",
    "tsc:w": "tsc -w",
    "lite": "lite-server",
    "typings": "typings",
    "postinstall": "typings install" 
  },
  "license": "ISC",
  "dependencies": {
    "angular2": "2.0.0-beta.13",
    "systemjs": "0.19.25",
    "es6-shim": "^0.35.0",
    "reflect-metadata": "0.1.2",
    "rxjs": "5.0.0-beta.2",
    "zone.js": "0.6.6"
  },
  "devDependencies": {
    "concurrently": "^2.0.0",
    "lite-server": "^2.1.0",
    "typescript": "^1.8.9",
    "typings":"^0.7.11"
  }
}
```
Install these packages by entering the following npm command in a terminal window (command window in Windows):

```sh
npm install
```

Node_modules are imported in you project directory you can see a folder named `node_modules` in your project directory.

Now we are all set with the environment development. 



Let's create a folder to hold our application and add super-simple angular component.

**Create an app sub-folder** of the root directory and make it the current directory

```sh
mkdir app
cd app
```

**Add a component file** named app.component.ts and paster the following line:

```sh
import {Component} from 'angular2/core';

@Component({
    selector: 'my-app',
    template: '<h1>My First Angular 2 App</h1>'
})
export class AppComponent { }
```

> **AppComponent is the root of the application**

Now we need something to tell Angular to load the root component

Add a new file , `main.ts`, to the `app/` folder as follows:

```sh
import {bootstrap}    from 'angular2/platform/browser';
import {AppComponent} from './app.component';

bootstrap(AppComponent);
```

Navigate to the **project root folder**.

```sh
cd ..
```

Create an `index.html` file in this root folder and paste the following lines:

```sh
<html>
  <head>
    <title>Angular 2 QuickStart</title>
    <meta name="viewport" content="width=device-width, initial-scale=1">    
    <link rel="stylesheet" href="styles.css">

    <!-- 1. Load libraries -->
    <!-- IE required polyfills, in this exact order -->
    <script src="node_modules/es6-shim/es6-shim.min.js"></script>
    <script src="node_modules/systemjs/dist/system-polyfills.js"></script>
    <script src="node_modules/angular2/es6/dev/src/testing/shims_for_IE.js"></script>   

    <script src="node_modules/angular2/bundles/angular2-polyfills.js"></script>
    <script src="node_modules/systemjs/dist/system.src.js"></script>
    <script src="node_modules/rxjs/bundles/Rx.js"></script>
    <script src="node_modules/angular2/bundles/angular2.dev.js"></script>

    <!-- 2. Configure SystemJS -->
    <script>
      System.config({
        packages: {        
          app: {
            format: 'register',
            defaultExtension: 'js'
          }
        }
      });
      System.import('app/main')
            .then(null, console.error.bind(console));
    </script>
  </head>

  <!-- 3. Display the application -->
  <body>
    <my-app>Loading...</my-app>
  </body>
</html>
```

>The System.import call tells SystemJS to import the main file (main.js ... after transpiling 
>main.ts, remember?). main is where we tell Angular to launch the application. We also catch and 
>log launch errors to the console.
>
>All other modules are loaded upon request either by an import statement or by Angular itself.
>
>**<my-app>**
>
>When Angular calls the bootstrap function in main.ts, it reads the AppComponent metadata, finds 
>the my-app selector, locates an element tag named my-app, and loads our application between 
>those tags.


Styles aren't essential but they're nice and the `index.html` assumes we have a stylesheet called `styles.css`.

Create a `styles.css` in the root folder and start styling, perhaps with this set:

```sh
/* Master Styles */
h1 {
  color: #369; 
  font-family: Arial, Helvetica, sans-serif;   
  font-size: 250%;
}
h2, h3 { 
  color: #444;
  font-family: Arial, Helvetica, sans-serif;   
  font-weight: lighter;
}
body { 
  margin: 2em; 
}
body, input[text], button { 
  color: #888; 
  font-family: Cambria, Georgia; 
}

/* 
 * See https://github.com/angular/angular.io/blob/master/public/docs/_examples/styles.css
 * for the full set of master styles used by the documentation samples
 */
```

### Compile and run

```sh
npm start
```

### Final Structure

Our final project folder structure looks like this:


.
+-- app
|   +-- begin-with-the-crazy-ideas.textile
|   +-- on-simplicity-in-technology.markdown
+-- node_modules ...
+-- typings ...
+-- index.html
+-- package.json
+-- styles.css
+-- tsconfig.json
+-- typings.json

Now yor first project is Created and All the best for the further Development on Angular 2 Cheer !!

For more info, tutorial and docs visit [Angular2 doc]. 

[node and npm]: <https://nodejs.org/en/download/>
[Angular2 doc]: <https://angular.io/docs/ts/latest/>

