# Setting Up a React / Vite App

## Installing on the Terminal

Using your terminal, and `npm`, a project manager for Node.js based projects. You'll want to include `Vite`, a development server that makes productions a lot faster.

To start, create a new app with Vite:

```bash
$ npm create vite@latest app-name --template react
```

This starts an app with the latest version of Vite and names the directory that holds the app. It will then ask you to select a framework, so choose React. It will then ask for a variant, so select JavaScript. From there, you just need to go into the directory and install the dependencies.

```bash
$ cd app-name

app-name$ npm install

app-name$ npm install sass

app-name$ npm install react-router-dom
```

React/Vite has depenedencies built in, and "npm install" installs all the boiler plate. The sass and react-router-dom packages aren't standard, but they're both important for development.

Once the dependencies are installed, run the command to start the production server:

```bash
app-name$ npm run dev
```

## Boiler Plate

There are a ton of folders and files there by default, but most of them aren't important for the majority of development.

### public

> The `public` directory is for assets that you want easy access to. Typically the only thing I keep there is the icon that shows up in the tab title, but it's also where you can store favicons, fonts, robots.txt files, or anything that doesn't need to be processed by build tools. The contents of your "public" folder will be available as-is in the main directory on bluehost.

### node_modules

> The `node_modules` folder is where all the dependencies are stored. They're here to make sure that all the functionality we want to use is running, but you shouldn't ever have to go in there yourself.

### src

> The most important folder, you'll be in here for the majority of your development time.

### index.html

> Your entire project is here. If you look in the body, you'll see the entire app is a \<div> element and a "module" script. The way React works is it creates components with functions, and executing those functions will dynamically populate the \<div> element with those components.

The rest of the files are configurations, but all the defaults are more than enough for what we're doing.

## Set Up

The `src` folder is where the bulk of your project is stored. The `assets` folder is similar to `public`, but it's for stylesheets, images, and scripts that are used throughout your components. Items in the `assets` folder are not directly available once the website is built, and it has a garbage collector so that unused assets are not loaded in the final build. 

### main.jsx

> There's no reason to edit this file, as it's just a simple container for The \<App /> component. It runs StrictMode, which is a production-only mode that runs in the background to check for pontential issues, so it's best to not mess with it.

### App.jsx

> This is your entire project. Components can be full of other components, and \<App /> is the component that houses all the other ones. If you open it now, you'll see all the elements that went live on the browser when you ran "npm run dev". 

The CSS files act like normal, being tied to their respective JSX files, but we won't be using them for these projects. Do not delete the files, as this can cause issues, but you can delete all their contents before you start your own project. 
