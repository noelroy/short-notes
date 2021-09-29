
# Vanilla JavaScript

***

## Modern Javascript Loading

In general script tags are placed inside head tag along woth other meta infos.

__Issue__ : When ever the brower sees a script, it stops html rendering and starting downloading and executing the javascript. This can cause issues if the html element on which the javascript is executed is not yet rendered.

__Solution__ : A simple solution is to place all those script tags after the body tag. In this case the script tags will be spread around in different places and this give rise to other issue

__Ideal Solution__ : Using `async` and `defer` keywords we can define how each script tag should behave. If async is provided, script file will be downloaded along with html rendering and the rendering task will stop only for the execution of the script/ If defer is used, the script will be downloaded in parallel to html rendering but script execution will happen only after the whole html is rendered.

>As a general guideline script tag should be specified in the header part and asyn/defer keywords should be used to control their execution.

***

## Javascript Modules

Modules can be used to separate out large code into different files.  
Step to create modules :
1. Separate out modular components to a separate file and export the component. Example :
    ```js
    const component_module = {
      name: "Everyday Backpack",
      volume: 30,
      color: "grey",
      pocketNum: 15,
    };
    export default component_module;
    ```
2. In the parent file import the component.
    ```js
    import component_module from "./ComponentModule.js"
    ```
3. In the html where these scipt tags are used, specify the type as module so that these scripts will be executed at the end of html rendering as fi defer keyword is specified.
    ```html
    <script type="module" src="ComponentModule.js"></script>
    <script type="module" src="script.js"></script>
    ```
> Note :  
>1. These modules will be available only in the context of the parent script file. So the `component_module` variable will not be accessible from the browser console.
>2. Modern JS Framework use modules heavily 

***

## Class construction

Object blueprint can be created in following ways

1. class keyword
```js
class Book {}
const Book = class {}
```

2. Object constructor function
```js
function Book(name) {
    this.name = name
}
```

Using class keyword allows us to extend othe classes

***

## Global Objects

All global objects can be found in the [MDN site](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects)


***

## Template Literals

Used to construct complex js strings.  
Eg: 
```js
const bookString = `The book has title ${booktitle} and has ${book.pages} pages` 
```

***
## DOM Manipulation

### Access DOM elements
1. `document.querySelector` : Returns a single element
2. `document.querySelectorAll` : Returns all elements that match 

we use [CSS selectors](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Selectors) to filter the dom elements required

### Modify element class
1. `Element.classname` : Modify class attribute as a whole string
2. `Element.classList` : Has methods to modify individual class names

### Attibutes
`Element.attributes` : Returns all attributes

Each element has attribute manipulation functions such as hasAttribute, getAttribute, setAttribute, remove Attribute

### Inline Style
`Element.style` : Returns all styles applied and can be modified individually using this object. The attribute names will be in camelCase intead of hyphens
Eg : `document.body.style.backgroundColor = "red"`

### Add DOM Element

1. `Document.createElement(tagName)` : create a new element but does not place it in DOM.  
    Eg : `document.createElement("article")`
2. `parentNode.append(nodes), parentNode.prepend(nodes)` : Add the element to the DOM. Comma separated multiple nodes can also be specified. HTML as string is also allowed.
3. `parentNode.appendChild()` : Same as above, but returns the child Node.

Other methods to add element to DOM includes `replaceChild`, `insertBefore`, `insertAdjacentElement(position, element)`

## Variable

`var` : function-scoped or globally-scope, mutable.  
`let` : block-scoped.  
`const`: block-scoped constant.

### Data Types 
Supports string, number, floating point, boolean, null, undefined, object and array
Use `typeof` to check data type of a variable

### Comparision
__==__ : loosely equal (does not check if type is same)  
__===__ : absolutly equal  
__**__ : to the power of

If one of the operands is a string, the operator `+` alone will act as a string concatinator.

## Arrays

Can hold a mix of any data type and we can assign values to indices higher than the current length.  
Eg :
```js
array = [1,"hi"]
array[9] = "out of length"
```

All supported array methods can be found in [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array#Instance_methods )

## Functions
1. Function Declaration : Classic way -  function hoisted to global scope.  
    Eg: `function exampleFunction () { }`  
2. Function expression : Assign an annonymous function to a variable.  
    Eg: `const exampleFunction =  function () { }`  
3. Annonymous Function  
    Eg : `(function () { })();`

### Arrow function expression  
Examples : 
```js
const exampleFunction =  (a) => { return a + 2 };
const exampleFunction =  (a) => a + 2;
const exampleFunction =  a => a + 2
```
 * Can be called only after its declared.
 * Arrow function doesnt have `this` and refers to the closest scope.  This is the reason why arrow function cannot be used for method declaration in a class/object. It will refer to the global scope instead of the method scope. Refer MDN for [more details](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions#this_and_Arrow_Functions)


## Conditional Switch Statement

We can replace a complex if statement with multiple conditionals to a conditional switch statement. Eg :
```js
switch(true){
    case age < 30 :
        description = "new";
        break;
    case age >= 30 && age < 365 :
        description = "lightly used";
        break;
    default:
        console.log("There is no condition") 
}
```

## Looping through content

Other than the normal iteration using an increasing pointer, following can also be used

### for...of loop and arrays
```js
for ( const item of stuff ){

} 
```

### foreach array method
```js
stuff.forEach((item) => {

});
```

### for...in lopp and objects
```js
for (const object in objects) {

}
```

## Events

Find list of all events in the [MDN website](https://developer.mozilla.org/en-US/docs/Web/Events)

Format : `target.addEventListener(event_type, callback [, options]);`

Using function declaration as callback will enable us to use the `this` variable. Arrow functions doesnt have `this` and refers to closest scope.  

The `event` object is automatically passed to the callback functino by the listener whenever it is fired.  

### How to pass additional arguments along with the event object to callback function

```js

function buttonToggle (event, param) {
    
}

button.addEventListener("click", (event) => {
    buttonToggle(event, additional_param)
})
```