#Angular

####Usefull angular cli commands 
+ ng new hello-world - Creates new hello-world application 
+ ng serve - Serves application on local server 

####Usefull VSCode short-cuts  
+ MAC
+ Windows
    + Shift+ctrl+P - Opens command palate 

####Folder structure  
+ E2E - Write E2E tests (Lauch browser, navigate, click something ...)
+ Node modules - 3rd party libs
+ src 
    + app 
        + module & component  
        + .editorcongit
        + .gitignore
        + karma.conf.js
        + package.json
            + dependencies
            + devDependencies 
        + ptotractor.conf.js
        + tsconfig.json - TS settings
        + tslint.json - lint settings    
    + Asstes - img, icon etc
    + environments - Prod & dev env
    + index.html
    + main.ts - starting point of an application 
    + polyfills.ts - loads scripts that are require to run application
    + Styles.cc - global style
    + test.ts -setting up testing env. 
    
    
####Webpack 
+ If something changes, Observer cli - webpack: Compiling  Angular cli used webpack, which is a build automation tool. It combines scripts and stylesheet into bundle.
+ Few bundles we can see in angular cli. After bulding below bundles, We can see the message Webpack compiled successfully 
    + polyfills.bundle.js - to fill the gap between js that angular needs & js that browser supports 
    + main.bundle.js - source code of our application 
    + styles.bundle.js - stylesheets in javascript. :D  
    + vendor.bundle.js - 3rd party libraries 
    + inline.bundle.js - 
+ Hot Module Replacement - When something changes, it reflects on browser 
+ Check source of app - we can see bundles in <script></script> tags. that means it is injected in index.html. Source code of index.html contains no reference to this. 
    
    
####Angular Version History 
+ AngularJS - 2010 js framework. Complex 
+ Angular 2 - 2016 Re-written. Typescript support
+ Angular 4 - TO align all the versions of libs, released angular 4. Example http, core version 2.x.x & router version was 3.x.x. In angular 4, versions were upgraded to 4