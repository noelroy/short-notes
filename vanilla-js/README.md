
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