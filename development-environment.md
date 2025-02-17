# Setting up an Angular Development Environment

- Make sure node and npm are installed
- Install Angular CLI (sudo npm install -g @angular/cli)
- Check version with ng --version
- Create new angular project with ng new [project name]
- To load application in a web server, run ng serve

# Project File Structure

- e2e: where we write end-to-end tests for the app
- node_modules: stores third-party libraries/dependencies
- src: source code of the application
    - app: contains modules and components
    - assets: stores static assets of application (images, icons, text files)
    - environments: configuration settings for different environments (production and development)
    - favicon.io: (favicon displayed in browser)
    - index.html: contains the angular application; styles etc. are dynamically inserted
    - main.ts: starting point of the application; similar to main() method
    - polyfills.ts: imports scripts required for running angular framework
    - styles.css: global application styles
    - test.ts: sets up testing environment
- configuration files such as angular-cli.json, editorconfig, gitignore, karma.conf.js, package.json, protractor.conf.js, tsconfig.json, tslint.json