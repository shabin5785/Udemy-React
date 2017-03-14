## How to get Help
- ste.grider@gmail.com
- Twitter: @sg_in_sf
- Github: github.com/stephengrider

Code link: https://github.com/StephenGrider/ReduxCasts

- An application will have our js files, then the libraries like react and redux. These are in ES6 format. No browser has complete support for ES6. Its a syntatically different Javascript. We have to transpile ES6 to browser js. We use Webpack and babel for this. So webpack+babel converts all our code to single file understood by browser

- React is a JS library. We write individual components or views. Components are snippets of code that produce html. Component is a set of JS functions that produce html

- Components by default are not put into view. We need to specifically include the components that we want to be in html

-Const is ES6 syntax. Const is declaring a variable as var. But const variable cannot be reassigned.

-jsx is a subset of javascript that allows to write HTML inside js. This is then transpiled to normal HTML.  JSX is a set of js code that produces html code.

-babeljs.io : view how es6 code looks in actual javascript..

-jsx components can be nested inside other components

-what we write in react is conveted to vanilla JS. go to the site given above to view that. We write html code inside react fns, that is converted to react specific vanilla js code.

- after we create the react components, we need to push them to the browser dom.

-React is diverging into two components. The core react library knows how to interact with react components.ReactDOM library is the one that now interacts with browser DOM.

- WHen we create a component we are creating a Class or a type of object. We are not acutally creating objects. We can create n number of objects from that class.

- the component class is converted to object when we use it as a tag. What react component does is actually declare a class of react tags, like html tags (div, h1 etc). Now use the component as it is means using the declaration. That is the class. So use the tag .
> const App = function () {
  return <divHi!</div;
}
React.render(App);
React.render(<App />);

Here first render gives error, as we are trying with a class. Second one is using an object.

- In above just render wont work. We have tell where to render it. Like a target container or dom. So needs to give a valid dom element in html document.

-component is a function or class that returns some html code. So we can have one component for search one for video, one for form etc

- So break up our app into components. Then design and implement them. Instead of having only one component. So basically we have one big components ( Our main page) and then multiple components nested inside that. We can have any levels of nesting

- Building components also helps us in reuse. Also one component per file is better

--Even if we are not using React element in a js file, if we are defining a react component in that file, we need to include React import, because when code is transpiled, the file with component will give error as it will be converted to react code and so React is needed to be included. To verify use the site to view react components and in js declare any react component and see the output code

-React components can be written as functional components (where we return a function that takes some input and return some html) or as es6 classes( class component). Class component has abilit to record its interaction or aware of its state, compared to fuctional component.

- ES6 class is a js object with functions and properties. Objects of that can be created using normal class objects using new operator.

-Every react class based component must have a render method to show it on screen

- Events are handled by event handlers and pass the event handler to the element we want to monitor. The custom handlers are linked using html triggers like onchange onFocus etc. This event object is inturn passed to the custom handler function. The event object passed has all details of the event.

-state is a plain js object that is used to record and react to user event. Each class based component that we defined has its own state object. when the components state changes it rerenders immediately.Also forces all his children to rerender as well.

- State needs to be initailized. Its a simple plain js object

- functional components do not have state. Only class based components do

- all js classes have a special fn called constructor. Like a java construtor. called when new instance is created. So we can define state inside that.

- always use setState or setProps. instead of using this.prop.key=''.. First one is the standard and correct way.Especially setting state. We always manipulate set using setState. setState infact tell react that value has changed. But we can use the getter only like this.props.key. Never use it to set.

-variable name has to be state. React state. nothing else.

- enclose js variables with {} while refering them inside jsx code


-  > render() {
    return (
      <div
      <input onChange={ (e) = this.setState({term: e.target.value}) } /
      Value of input : {this.state.term}
    </div
    );
    
    Now when input changes,event listener runs. This updates the state. This causes the element to rerender. This inturn invokes render method. Render method has a line to print the state causing new value to be shown.
    
    