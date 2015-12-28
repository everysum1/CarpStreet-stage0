# MAKING A REACT WEB APP BOILERPLATE

## Goal
Creating and deploying to Heroku the most barebone React app.

## Steps to creating the app:

0. Install modules
    - Run **"npm install"** to install the modules in package.json
    - Run **"sudo npm install webpack -g"** so that we'll be able to run "webpack..." from the command line.  
    - Run **"sudo npm install webpack-dev-server -g"** so that we'll be able to run "webpack-dev-server..." from the command line.  

1. State which modules are needed
    - Create *package.json*, which states which libraries are required by the app.
    - Fill it with the most basic libraries: react, babel, babel-loader, webpack. 

2. Write an entry point JS/JSX file
    - Create a file that "kicks off" the application. *src/entry.jsx* here.
    - In *entry.jsx*, require react.

3. Kick off the auto-build process (Webpack here).
    Because our react code live in multiple JS/JSX files, they need to be bundled/compiled/built into a single JS file before it can be used. It's a good idea to kick off an automatic build process before writing actual code, so that we know as soon as something breaks.
    - We use Webpack here. Some use Gulp instead.
    - A config file is needed to instruct Webpack on how to actually build our application. It's like a makefile in the C/C++ world.
    - Create *webpack-dev.config.js* (for dev) and *webpack-prod.config.js* (for prod) here. See samples.
    - point the output to *bundle.js*.
    - Run **"webpack-dev-server --config ./webpack-dev.config.js --progress --colors"** for continuous auto-build.
    - Errors, if any, will be printed out fully at *http://localhost:8080/webpack-dev-server/*. 

4. Create index.html that has a script tag pointing to the *bundle.js* file that was created in the previous step 

Actually have "Hello, JJ." show up on the webpage.

## Deploying to Heroku

### Setting Heroku Env variables
**heroku config:set NODE_ENV=production**

### What don't need to be / shouldn't be deployed:
- node_modules
    Since Heroku may have a different environment from our local machine, package.json will tell heroku which modules are required.
- public/bundle.js
    This file is huge and will be created on the Heroku end, instructed by the *script* section in *package.json*.

