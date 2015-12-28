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
    - In *entry.jsx*, require react, render "hello world" (see sample).

3. Kick off the auto-build process (Webpack here).
    Because our react code live in multiple JS/JSX files, they need to be bundled/compiled/built into a single JS file before it can be used. It's a good idea to kick off an automatic build process before writing actual code, so that we know as soon as something breaks.
    - We use Webpack here. Some use Gulp instead.
    - A config file is needed to instruct Webpack on how to actually build our application. It's like a makefile in the C/C++ world.
    - Create *webpack-dev.config.js* (for dev) and *webpack-prod.config.js* (for prod) here. See samples.
    - point the output to *bundle.js*.
    - Run **"webpack-dev-server --config ./webpack-dev.config.js --port <portnumber> --inline"** for continuous auto-build and auto browser-refresh.
    - Go to *http://localhost:<portnumber>/public* to see the webpage. Error, if any, will be shown in full there.  

4. Create index.html that has a script tag pointing to the *bundle.js* file that was created in the previous step 

5. Get scss styles to work
    - create *css/app.scss*
    - require it in entry.jsx

## Deploying to Heroku

1. Setting Heroku Env variables
    **heroku config:set NODE_ENV=production**

2. Create a server.js file to serve index.html.
    - We use express server here. But really anything that serves index.html would work fine (python, ruby, etc.).

3. Add to package.json a *postinstall* script that:
    - runs webpack to produce bundle.js on the Heroku machine
    - starts the express server ("node server.js" is assumed by Heroku if this line in package.json were missing.) 


### What don't need to be / shouldn't be deployed:
- node_modules:
    Since Heroku may have a different environment from our local machine, package.json will tell heroku which modules are required.
- public/bundle.js:
    This file is huge and will be created on the Heroku end, instructed by the *script* section in *package.json*.
- webpack-dev.config.js:
    For the obvious reason that the production environment doesn't care about dev configs.

### Quick debugging/diagnosis of Heroku
A few tools that are really quick and useful for checking out what's going on on the heroku side:

- **heroku logs --tail**:
    - shows heroku logs

- **heroku bash**:
    - lets you access the heroku bash shell, where you can see files, run commands, etc.

## Gotchas
- webpack-dev-server does NOT change bundle.js. Instead, it serves from cached memory. Run *webpack* instead if you need it changed.