#Angular

####Usefull angular cli commands 
+ ng new hello-world - Creates new hello-world application 
+ ng serve - Serves application on local server 

####Usefull VSCode short-cuts  
+ MAC
+ Windows
    + Shift+ctrl+P - Opens command palate 
    + F2 - Rename

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
        
       
    }
    
    Now I don't have to declare class level variable x & then in constrcutor this.x = x.
    Typescript will take care of it. (If Access modifiers in constuctor parameters is used) 
    If u use public, then u will be able to modify x.
    point.x = 10; 
    ```
+ Properties

 ```
    class Point{
        
       ...
       
        getX(){
            return this.x;
        }
        
        setX(value){
            this.x = value;
        }
    }
    
    NOTE: Use properties instead of getter , setter. 
    
    get X(){
        return this.x;
    }
    
    set X(value){
        this.x = value;
    }
    
    Now, instead of point.setX(10), You can do point.X = 10; 
    ** If get x is used instead of X, It will thorw a compile time error. because of 
    constructor(private x:number){...}
   
   Properties looks like property from outside but its really a method from inside 
 ```
+ Modules
    + We can say file as a module when it is visible from outside. To make file module - export it. When file is exported, import it. 
    + Anything can be exported, feild, methods, classes etc. 
     
     
#### Angular Fundamentals 
##### Building Blocks Of Angular
+ Components - Encapsulates data, html, logic for view. App is made up of 1 or more components. Every app has app component, and app is a tree starting from app component
+ Modules - Container, or group of related component. Every app has app module.
+ Directives - We use directive to manipulate DOM, Example ngFor="", Use it like attribute in html. 
 prefix directive which will manipulate DOM with *. Reason ? -
+ Services -  
    + Logic to calling http service in component
        + Problem - Service would be tightly coupled , hence problem in unit testing.(Dependency of HTTP)
        + Problem - Somewhere in app we may want to invoke this service. So logic will be repeated.
        + Component should not include logic other than a presentation logic. 
    + New file - *.service.ts (Convention) 
    + export class - export *Service{}
    + getCourses method with logic in it
    + Dependency Injection - 
        + In order to consume service in component, use constructor() to initialize service & data of service.
    Now, as in constructor of component, we have written a statement like = new *Servive(); , Now, is is tightly coupling.
        + And by chance, If we change structure of service constructor, Where ever the service is used, compiler will cry. 
        + So, Add parameter in component constructor. (Inject service in component constructor. )
        + Now, 2nd advantage is, Whenever we need to unit test component, If we would have used = new *Service in constructor. We would have to give actual implementatiion. Now as we have injected dependency, we can fake its implementation in unit testing. 
        + To instruct angular to inject service, app.module -> provider[] -> register dependencies, (as *Service is dependent on *Component). If you forget this, dependency injection wont work. Error -> No providers for *Service
        + app.module -> provider -> service resisted -> singleton. 
    + ng generate service * OR ng g s *. 
        + *.service.ts
            + Now, extra @Injectable() on class level. Why ? When service needs extra dependencies in its constrcutor. (Ex- logService, http)
            + Now, This class is injectable class, means angular should be able to inject dependencies in it. So Why we did not use this in Component? because component internally call Injectable. 
        + *.service.spec.ts
    
###Displaying data and handling events       
####Property Binding
+ Interpolaton means {{}}
+ Interpolation is syntactical sugar, behind the scenes angular translates intopolation in property binding, Binding property of a DOM element like src="..." to feild or property in our component. 
```
<img [src]="imageUrl" > // we are not using interpolation i.e {{}} here.
// We want src value to be bind with imageUrl from component. 
<img src = {{imageUrl}}> Equvivalent
```
+ When to use interpolation or when to use property binding
```
<h2 [textContent]="title"></h2> // NOISY 
<h2><{{"title"}}/> // Shorter and cleaner. 
```
+ [] and feild name name 
+ NOTE: Property binding works only one way.  from componet to DOM. So any changes from DOM won't be reflected in here. 

####Attribute Binding
+ Suppose we have <td [colspan]="colSpan"/>, Error - Can't bind to colspan since it isnt a known property of td
+ DOM(Document Object model) vs HTML 
    + DOM - Tree of objects, like html --> head --> title, script. i.e tree of objects in memory
    + HTML - Markup language used to represent DOM in text. 
    + Most of the attributes of html elements (for example src from <img></img> ) have one to one mapping with DOM elements. But there are html attributes that dont have representation in DOM. Example colspan. 
    + Also, we have properties in DOM that do not have representation in HTML. example <h1 [textContent]='title'/> we don't have textContent in html. 
    + <td [attr.colspan]="colSpan"/>
     
####Adding Bootstrap 
+ getbootstrap.com
+ Now, terminal --> style.bundle.js --> 10kb
+ npm install bootstrap --save (download in node modules and make entry in package.json )
+ styles.css - import bootstrap.css from node modules 
+ Now, styles.bundle.js size 159 KB

####Class binding
+ add classes based on condition 
```
<button class="btn btn-primary" [class.active]="isActive">Save</button>
```
Now, if isActive feild from typescript is set to true then, active css class is included in style. if false then active css class won't be applied. 
So, If if isAtcive is true then, [btn , btn-primary, active] css classes will be applied. 

NOTE: For class binding we use property binding variation. hence [ ] is used

####Style binding
Also, variation in property binding, very similar to class binding. If developer wants to apply styles based on condition.

```
<button [style.x]="isActive ? 'blue' : 'white' "/>

x -> any propery of dom object, Example backgroundColor. For complete list of all the properties of style object. search "DOM  style object properties" on Google, w3schools has the list. 

<button [style.backgroundColor]="isActive ? 'blue' : 'white' "/>
```

####Event binding
+ to handle events raised on the DOM. 
+ use ( )
```
<button (click)="onSave()">save</button>

onSave() method in component


// This will invoke onSave(). 
```

To access Event object, add parameter to onSave()

```
<button (click)="onSave($event)">save</button>

onSave($event) method in component
```

+ $event represents standard DOM event, (seen in vanila js, jQuery)
+ Custom events also can be make.
+ All the DOM events bubble up the DOM tree, unless handler prevents further bubbling. This is standard event propogation mechanism in DOM. Example:
```
<div (click)="onDivClicked()"
  <div (click)="onDivClicked()"
    <button (click)="onSave($event)">save</button>
  </div>  
</div>  


$event - this object will bubble up and hit the outer div. 
TO STOP
    - onSave($event){
        $event.stopPropogation();
    }
    
// THis will not invoke onDivClicked()     
```


####Event filtering
+ On ENTER, Do something
    + Traditional Way
        ```
            <input (keyup)="onKeyUp($event)"/>
            
            onKeyUp($event){
                if($event.keyCode ===13) console.log("ENTER PRESSED")
            }
        ```
        
    + Angular way
        ```
            <input (keyup.enter)="onKeyUp()"/> // NO NEED TO PASS event
                    
            onKeyUp(){
               // No ceromony. It will invoke only on pressing enter
            }
        ```

#####Template Variables
To get the value we are giving to input.
```
    <input (keyup.enter)="onKeyUp($event)"/>
           
    onKeyUp($event){
      console.log($event.target.value)
    }
```

Using template variable
```
    <input #email (keyup.enter)="onKeyUp(email.value)"/>
           
    onKeyUp(email){
      console.log(email)
    }
```
        
####Two way binding. 
+ Passing objects - also carries some data, some behaviour - procedural programming. Not recommended 
```
<input [(ngModel)]="email" (keyup.enter)="onKeyUp()"/>
           
    email="xyz.abc"       
           
    onKeyUp(){
      console.log(this.email)
    }
    
    - [()] Banana in a box syntax 
    - ngModel - Why ? Input DOM object does not have propertry called ngModel. This is something that angular adds to DOM object.
    (Directive - to manipulate DOM)
    - ngModel is in form module. app.module.ts -> @NgModel -> imports -> FormsModule. 
```       
  
####Pipes
+ To format data
+ Built in pipes- Uppercase, Lowercase, Decimal, Currancy, Percent
+ Example - {{ title | uppercase}}, {{price | currency}} -> USD . To change it to AUS dollar. {{price | currency:'AUD':true}} // :true to display symbol

####Custom Pipes
+ New file summary.pipe.ts
+ import Pipe, PipeTransform from core
+ @Pipe({ name: 'summary'})
+ export SummaryPipe implements PipeTransform
+ transform(value: any, args?: any){ // business logic }
+ Just like component, service, we need  to register pipe in module. @NgModule({declarations : [SummaryPipe]})
+ TO USE : {{text | summary}}
+ TO SUPPLY ARGUMENTS : transform(value: any, limit?: number){ // business logic }
Now, {{ text | summary:50 }}. We can add more parameters to this.

###Building Reusable components

####Component API
+ Input Property
    + 1st Approach 
        + Annotate feild with @Input. Example isFavorite.
        + To input this component
        ```
        <favorite [isFavorite]="true"></favorite>
        ```
    + In component decorator,
        ```
        @Component({
        selector: 'favorite',
        ...
        inputs: ['isFavorite']
        })
        ```
        + If someone refactor renames isFavourite, ['isFavorite'] will not be updated. NOT RECOMMENDED. 
    + Aliasing input property.
        + @Input('is-favorite')
        + If someone refactors and renames iSFavorite, App will break because,  <favorite [isFavorite]="true"></favorite> is not refactoed. Hence alising is a good idea. 
+ Output          
    + favourite component raise a custom event - onFavoriteChanged() 
    + add a method in favorite component -  onFavoriteChanged()
    ```
     <favorite [isFavorite]="true" (change)="onFavChange()"></favorite>
     
     // in implementation of onFavChange(). Event change will be notified.


     @Output() change = new EventEmitter();
     
     onClick(){
     
     this.change.emit();
     }
    ```
+ Passing Event Data
     ```
     <favorite [isFavorite]="true" (change)="onFavChange($event)"></favorite>
     
     // in implementation of onFavChange($event). Event change will be notified.
     // $event - anything that we pass, not standard DOM event. 
     // here boolean is passed, we can pass anything
     // **** We can specify type of argument to pass. We can specify interface to specify type
     
     ....
     
     @Output() change = new EventEmitter();
         
     onClick(){
         
       this.change.emit(this.isSelected); // Subscriber will have values 
     }
     
     
     
     ```
+ Aliasing Output Properties      
    + @Output() change = new EventEmitter(); If you change - change, app will break, hence alising would be better. 
    + @Output('change') - DONE

+ Templates 
    + use either templateUrl or template
    + Developer console - Network - main.bundle.js -> html code
    
+ Styles - 3 ways to apply styles 
    + styleUrls in @component
    + styles: [
        ``
            css goes here
        `
    ] 
    + Inline in html templates 
    + NOTE: The one that comes last in @component. Only applies styles from last thing, It will completly ignore all other styles. 
    
+ View encapsulation 
    + styles applied in components are scoped in that component
    + Shadow DOM
        + It is a specification that enables DOM tree and style encapsulation  
        + Allows us to apply scoped styles to elements without bleeding out to the outer world
        + @Component({ encapsulation: ViewEncapsulation.Emulated })
            + Emulated - Emulates shadow DOM (Default - No need to change)
            + Native - Uses Shadow DOM , Which wont work in many browers. Chrome higher & Safari 10+.
            + None- No shadow DOM encapsulation  
 
+ ngContent
    ```
    <div>
        <div class="heading"></div> // I want to pass heading text from outside 
        <div class="heading"></div> // I want to pass body text from outside 
    </div>
    
    //Not using property binding to achiev this.
    ```        
    ngContent
    ```
        <div>
            <div class="heading">
                <ng-content select=".heading"></ng-content>
            </div>  
            <div class="body">
                <ng-content select=".body"></ng-content>
            </div>  
        </div>
        
        //Select is identifier and its value is matcher 
        
        
        <component>
          <ng-container class="heading">abcdef...</ng-container>          // It will replace ng-conent. class is matcher
          <ng-container class="body"> ....complext-html....</ng-container> // Noise of extra div reduced. In previous example if you inspect, there will be div under div. Now, content under div      
        </component>
        
    ```              
    
ngContainer    

 ```
    <div>
        <div class="heading"></div> // I want to pass heading text from outside 
        <div class="heading"></div> // I want to pass body text from outside 
    </div>
    
    //Not using property binding to achiev this.
 ```        
 ngContent
 ```
        <div>
            <div class="heading">
                <ng-content select=".heading"></ng-content>
            </div>  
            <div class="body">
                <ng-content select=".body"></ng-content>
            </div>  
        </div>
        
        //Select is identifier and its value is matcher 
        
        
        <component>
          <div class="heading">abcdef...</div>          // It will replace ng-conent. class is matcher
          <div class="body"> ....complext-html....</div> // We can add complex struture here       
        </component>
        
        // no need of selector only if you have 1 ng-content
 ```     
    
##Directives 

+ Directives - to modify the DOM
    + Structural - Modifies the  structure of the DOM (Whenever using prefix it with *)
    + Attribute - Modifies the attribute of DOM elements

###ngIf

```
<div *ngIf="doWeHaveAnyContent()"
    ...
</div>
```    

// **** If condition is truthy, It will be added to DOM otherwise It will be removed from the DOM. Inspect this.

If else 

```
<div *ngIf="doWeHaveAnyContent() ; else noContent"
    ...
</div>   

<ng-template #noContent">
    ... empty msg ...
</ng0template>   
```

// if content is present - upper DOM, if not lower DOM
Like above example, we can use if-then-else using template variable and ng-template 


###Hidden attribute

+ hidden also exists in DOM as property 
+ Do property binding 

```
<div [hidden]="hide is some cond evaluates to true">

</div>
```

+ DIFFERENCE between ngIf & hidden
    + ngIf - If condition evaluates to falsy, element is removed from the DOM
    + hidden - keeps all elements in DOM but some are hidden based on condition
+ Better ? - If large no of elements are there
    + Memory in the DOM issue when too many elements (better to use ngIf). 
    + Load to change detection mechanism in angular.   
    + Large tree, When frequent toggle operations are there, ngIf might be costly so use hidden and keep elements in DOM
+      
    
### ngSwitch Case

+ Property Binding 
+ If you want to compare value against multiple values.

```
viewMode = "Map";


<ul>
    <li [class.active]="'map'">....
    <li [class.active]="'list'">....
</ul>

<div [ngSwitch]="viewMode"> 
    <div *ngSwitchCase="'map'"> some map content </div>
    <div *ngSwitchCase="'map'"> some view content </div>
    <div *ngSwitchDefault> Otherwise </div> //no value to default
</div>

```

###ngFor

```
Component - 

courses = [
    { id:1, name:'course1'},
    { id:1, name:'course2'},
    { id:1, name:'course3'}
];



<ul>
    <li *ngFor = "let c of courses">
        {{course.name}}
    </li>
</ul>


// Highlight - 1st row OR last row OR index OR odd rows
For above purpose, we need to use exported values, so index is one of them, & we will assign it to local variable
<ul>
    <li *ngFor = "let c of courses; index as i">
        {{course.name}} - {{i}}
    </li>
</ul>


******* List of all exported values ************

angular.io -> serach - ngForOf(actual name of ngFor is ngForOf)
-> under local variables, you will find all exported values  


**** Use even, odd, first as isEven, isOdd, isFirst **** 

```

+ ngFor and change detection - 
    + AJAX, Change event, 
+ Developer console - purpul blink - change detection 


+ Scenario 
    + Button click - onButtonClick - array initialization
    + Every time button is clicked, Even though content is same new objects with new memory locations will be initialised. 
    + So, to avoid it, use reference identity . 
    ```
    <ul>
        <li *ngFor="let course of courses; trackBy: trackCourse">
        
        </li>
    </ul>
    
    
    
    trackCourse(index, course){
       return course ? course.id : undefinded;
    }
    ```        
    + Now, no longer purple highlight that means, no change detection 
    + Simple list - no worrier, angular performs out of the box, complex - optimise change detection.
     
### Leading asterisk 
+ When you use * in directives - You are telling angular to rewrite block using ng-template. 
     
     
###ngClass 
     
```
In object => 
key -> css class
value -> boolean - should render the css or not

ngClass -> Example of an attribute directive, used to modify an attribute in existing DOM element 

//TODO without using ngClass example

<span [ngClass]="{
    'glyphicon-star' : isSelected,
    'glyphicon-star-empty' : !isSelected
}"
```


###ngStyle 

```
key -> css style
value -> style value

<button 

    [style.backgroundColor]="canSave ? 'blue' : 'gray'"
    [style.color]="canSave ? 'white' : 'black'"
 
    [ngStyle]="{
        'backgroundColor' : canSave ? 'blue' : 'gray',
        'color' : canSave ? 'white' : 'black',
    }"

```

###Safe traversal operator 

+ When traversing through complex object, object can be undefined or null for fraction of a second
    + Error TypeError: can not read property 'name' of null 
+ 2 ways to solve it 
    + ngIf to check null. ELEMENT WONT BE IN DOM     
    + ? -> angular reads it as it can be null so, angular ignores it. ELEMENT AVAILABLE IN DOM
    
    
### NOTES 
+ HostListener from core accepts the dom evenet 
  ```
  @HostListener('blue') onBlur() // Blur - when you click on the element
  ```
+ ElementRef - service provided by angular to access DOM objects  
  Example :- this.elementRef.nativeElement (String format etc.)
  
    
###Custom Directives (REVISIT)
+ ng g d name - ng generate directive name
    + ts file
    + spec file
    + It will update app.module.ts -> @NgModule - declarations - new entry 
    + NOTE : component, pipes, directives (Which are part of the directive)- should be declared in @NgModule declarations
    + selector : '[appInputFormat]' 
    + Business logic 