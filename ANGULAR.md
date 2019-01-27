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
    + Assets - img, icon etc
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

####Typescript 

+ Typescript - superset of javascript. Supports strong typing(Optional), Object oriented features - classes, interfaces, generics etc. Catches errors at compile time. 
+ TypeScript --> Transplie --> Javascript 
+ Install & run typescript 
    + npm install -g typescript 
    + tsc -- version (Typescript compiler)
    + tsc main.ts 
    + If you ls - main.js, main.ts 
    + node main.js . It runs that means valid typescript code is valid js code
    + When you run ng serve, angular cli runs transpiler under the hood. 
+ Typescript variable declaration 
   + var , In below example i is accessible outside for. Accessible in nearest function
   ```javascript
   function doSomething(){
        for(var i = 0; i<5 ; i++){
            console.log(i);
        }
        console.log('Finally : '+i)
   }
   
   // Output
   0
   1
   2
   3
   4
   Finally 5
   ```
   + let (ES6 has it) Accessible in nearest block. So not outside of for
    ```javascript
      function doSomething(){
           for(let i = 0; i<5 ; i++){
               console.log(i);
           }
           console.log('Finally : '+i) // compile time error
      }
    ```
    + Transpiler by default converts TS to ES5. Which does not have let keyword. 
    + Use let over var
+ Types
    + let a : any;
    + let a :number; // integer, floating point 
    + let a : boolean; // true, false
    + let a : string;
    + Array -let a: number[] = [1,2,3,4,5], let b: any[] = [1. 2. "a", false]
    + Enum -
    ```
    enum Color{Red = 0, Green = 1, Blue = 1};
    let backGroundColor = Color.Red; 
    
    // If u comiple it, In js u can see the code function(Color)...
    ```
    + const red = 0;
+ Type assertions 
    + let message = 'abc'; message.endsWith('c') // U get intelligence here but if u declare message and then initialise it in 2nd line, message type becomes any. So u wont get any intellisense. 
        + Solution 1. (<string>message).endsWith('c'); // Intelligence available
        + Solution 2. (message as string).endsWith('c'); // Intelligence available
        NOTE: It doesnt change anything except we get Intelligence. 
+ Arrow functions 
    + JavaScript
    ```
    let log = function(message){
        console.log(message);
    }
    ```
    + TypeScript    
    ```
    let doLog = (message) =>{
        console.log(message);
    }
    
    let doLog = (message) => console.log(message);
    // for singe line {} is not neccessary, but it will break
    ```
+ Interface 
    + 
    ``` 
    let drawPoint = (point) => {//...}
    drawPoint({x:1,y:2}) // No compile time error
    ```
    Inline annotation
    ``` 
    let drawPoint = (point : {x: number, y: number}) => {//...}
    drawPoint({x:1,y:2}) // No compile time error
    ```
    Interface
    ``` 
    interface Point{
        x:number;
        y:number;
    }
    
    let drawPoint = (point : Point) => {//...}
    drawPoint({x:1,y:2}) // No compile time error
    ```

+ Classes
    + Cohesion - related things should be part of same unit, They should go together
    + In interfaces example, we have violated cohesion principle. Point and drawPoint should be part of same unit - class
    + To apply, use class instead interface
    ```
       class Point{
        x: number;
        y: number;
        
        draw(){
        
        }
       }
    ```

+ Objects 
    ```
    let point : Point; 
    point.x = 1; ....
    point.draw(); // draw() -> undefined
    
    
    let point : new Point(); 
    point.x = 1; ....
    point.draw(); // OK
    
    OR
    
    let point : Point = new Point();
    point.x = 1; ....
    point.draw(); // OK . NOISE -------- : Point 
    ```
+ Constructor 
    ```
     class Point{
            x: number;
            y: number;
            
            constructor(x:number, y:number){ // Constructor - keyword 
                // initialize here x & y
            }
            
            draw(){
            
            }
     }
        
     let point : new Point(1,2); 
     point.draw();      
           
    ```
    + Like java, We can't have multiple constructors, So solution is to make parameters optional.
    + Once, You make 1 parameter optional, all the parameters at the right side should also be optional. 
     hence if we want to make x optional , we have to make y optional .
     
    ```
         constructor(x?:number, y?:number){  
                       // initialize here x & y
         }  
            
    let point : new Point(); // No compilation error         
    ```
    
+ Access modifiers 
    + public - (By default - public, so applying public is redundant)
    + private - (Only accessible within class)
    + protected 
    + Access modifiers in constuctor parameters 
    ```
    class Point{
        
        constructor(private x:number){
        
        }
        
        draw(){
        
        }
        
        getX(){
            return this.x;
        }
        
        setX(){
        
        }
    }
    
    Now I don't have to declare class level variable x & then in constrcutor this.x = x.
    Typescript will take care of it. (If Access modifiers in constuctor parameters is used) 
    If u use public, then u will be able to modify x.
    point.x = 10; 
    ```
    