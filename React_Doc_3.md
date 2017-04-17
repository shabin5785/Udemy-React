- The first part of a JSX tag determines the type of the React element.
Capitalized types indicate that the JSX tag is referring to a React component. These tags get compiled into a direct reference to the named variable, so if you use the JSX <Foo /> expression, Foo must be in scope.

- Since JSX compiles into calls to React.createElement, the React library must also always be in scope from your JSX code. So even if we are not directly referring to React, as we are using JSX React must be in scope

- You can also refer to a React component using dot-notation from within JSX. This is convenient if you have a single module that exports many React components. For example, if MyComponents.DatePicker is a component, you can use it directly from JSX 
> function BlueDatePicker() {
  return <MyComponents.DatePicker color="blue" /;
}

- When an element type starts with a lowercase letter, it refers to a built-in component like <div> or <span> and results in a string 'div' or 'span' passed to React.createElement. Types that start with a capital letter like <Foo /> compile to React.createElement(Foo) and correspond to a component defined or imported in your JavaScript file.
We recommend naming components with a capital letter. If you do have a component that starts with a lowercase letter, assign it to a capitalized variable before using it in JSX.

> // Wrong! This is a component and should have been capitalized:
function hello(props) {
  // Correct! This use of <div is legitimate because div is a valid HTML tag:
  return <divHello {props.toWhat}</div;
}
function HelloWorld() {
  // Wrong! React thinks <hello /> is an HTML tag because it's not capitalized:
  return <hello toWhat="World" />;
}

To fix this, we will rename hello to Hello and use <Hello /> when referring to it:

- You cannot use a general expression as the React element type. If you do want to use a general expression to indicate the type of the element, just assign it to a capitalized variable first. This often comes up when you want to render a different component based on a prop:
> function Story(props) {
  // Wrong! JSX type can't be an expression.
  return <components[props.storyType] story={props.story} /;
}

To fix this, we will assign the type to a capitalized variable first:
> function Story(props) {
  // Correct! JSX type can be a capitalized variable.
  const SpecificStory = components[props.storyType];
  return <SpecificStory story={props.story} /;
}

### Props in JSX

There are several different ways to specify props in JSX.

-You can pass any JavaScript expression as a prop, by surrounding it with {}. For example, in this JSX:
<MyComponent foo={1 + 2 + 3 + 4} />
For MyComponent, the value of props.foo will be 10 

if statements and for loops are not expressions in JavaScript, so they can't be used in JSX directly. Instead, you can put these in the surrounding code.

> function NumberDescriber(props) {
  let description;
  if (props.number % 2 == 0) {
    description = <strongeven</strong;
  } else {
    description = <iodd</i;
  }
  return <div{props.number} is an {description} number</div;
}

- You can pass a string literal as a prop. These two JSX expressions are equivalent:

<MyComponent message="hello world" />
<MyComponent message={'hello world'} />

When you pass a string literal, its value is HTML-unescaped. So these two JSX expressions are equivalent:

<MyComponent message="&lt;3" />
<MyComponent message={'<3'} />

- If you pass no value for a prop, it defaults to true. These two JSX expressions are equivalent:

<MyTextBox autocomplete />
<MyTextBox autocomplete={true} />

In general, we don't recommend using this because it can be confused with the ES6 object shorthand {foo} which is short for {foo: foo} rather than {foo: true}. This behavior is just there so that it matches the behavior of HTML.

- If you already have props as an object, and you want to pass it in JSX, you can use ... as a "spread" operator to pass the whole props object. These two components are equivalent:

> function App1() {
  return <Greeting firstName="Ben" lastName="Hector" /;
}
function App2() {
  const props = {firstName: 'Ben', lastName: 'Hector'};
  return <Greeting {...props} /;
}

Spread attributes can be useful when you are building generic containers. However, they can also make your code messy by making it easy to pass a lot of irrelevant props to components that don't care about them. 

### Children in JSX

In JSX expressions that contain both an opening tag and a closing tag, the content between those tags is passed as a special prop: props.children. There are several different ways to pass children:

- You can put a string between the opening and closing tags and props.children will just be that string. This is useful for many of the built-in HTML elements. For example:
<MyComponent>Hello world!</MyComponent>
This is valid JSX, and props.children in MyComponent will simply be the string "Hello world!". HTML is unescaped, so you can generally write JSX just like you would write HTML in this way:

- JSX removes whitespace at the beginning and ending of a line. It also removes blank lines. New lines adjacent to tags are removed; new lines that occur in the middle of string literals are condensed into a single space. 

- You can provide more JSX elements as the children. This is useful for displaying nested components:

<MyContainer>
  <MyFirstComponent />
  <MySecondComponent />
</MyContainer>
You can mix together different types of children, so you can use string literals together with JSX children. 

A React component can't return multiple React elements, but a single JSX expression can have multiple children, so if you want a component to render multiple things you can wrap it in a div like this.

- You can pass any JavaScript expression as children, by enclosing it within {}. For example, these expressions are equivalent:

<MyComponent>foo</MyComponent>

<MyComponent>{'foo'}</MyComponent>
This is often useful for rendering a list of JSX expressions of arbitrary length. For example, this renders an HTML list:

> function Item(props) {
  return <li{props.message}</li;
}
function TodoList() {
  const todos = ['finish doc', 'submit pr', 'nag dan to review'];
  return (
    <ul
      {todos.map((message) = <Item key={message} message={message} /)}
    </ul
  );
}

JavaScript expressions can be mixed with other types of children. This is often useful in lieu of string templates:

> function Hello(props) {
  return <divHello {props.addressee}!</div;
}

- Functions as Children
Normally, JavaScript expressions inserted in JSX will evaluate to a string, a React element, or a list of those things. However, props.children works just like any other prop in that it can pass any sort of data, not just the sorts that React knows how to render.

-false, null, undefined, and true are valid children. They simply don't render. This can be useful to conditionally render React elements. 
One caveat is that some "falsy" values, such as the 0 number, are still rendered by React. For example, this code will not behave as you might expect because 0 will be printed when props.messages is an empty array:

> <div
  {props.messages.length &&
    <MessageList messages={props.messages} /
  }
</div
To fix this, make sure that the expression before && is always boolean:
<div
  {props.messages.length  0 &&
    <MessageList messages={props.messages} /
  }
</div

Conversely, if you want a value like false, true, null, or undefined to appear in the output, you have to convert it to a string first:

<div>
  My JavaScript variable is {String(myVariable)}.
</div>


### Refs and the DOM

-In the typical React dataflow, props are the only way that parent components interact with their children. To modify a child, you re-render it with new props. However, there are a few cases where you need to imperatively modify a child outside of the typical dataflow. The child to be modified could be an instance of a React component, or it could be a DOM element. For both of these cases, React provides an escape hatch.

-There are a few good use cases for refs:

Managing focus, text selection, or media playback.
Triggering imperative animations.
Integrating with third-party DOM libraries.
Avoid using refs for anything that can be done declaratively.

For example, instead of exposing open() and close() methods on a Dialog component, pass an isOpen prop to it.

-React supports a special attribute that you can attach to any component. The ref attribute takes a callback function, and the callback will be executed immediately after the component is mounted or unmounted.

When the ref attribute is used on an HTML element, the ref callback receives the underlying DOM element as its argument. For example, this code uses the ref callback to store a reference to a DOM node:

> class CustomTextInput extends React.Component {
  constructor(props) {
    super(props);
    this.focus = this.focus.bind(this);
  }
  focus() {
    // Explicitly focus the text input using the raw DOM API
    this.textInput.focus();
  }
  render() {
    // Use the `ref` callback to store a reference to the text input DOM
    // element in an instance field (for example, this.textInput).
    return (
      <div
        <input
          type="text"
          ref={(input) = { this.textInput = input; }} /
        <input
          type="button"
          value="Focus the text input"
          onClick={this.focus}
        /
      </div
    );
  }
}

React will call the ref callback with the DOM element when the component mounts, and call it with null when it unmounts.

Using the ref callback just to set a property on the class is a common pattern for accessing DOM elements. The preferred way is to set the property in the ref callback like in the above example. There is even a shorter way to write it: ref={input => this.textInput = input}.

When the ref attribute is used on a custom component declared as a class, the ref callback receives the mounted instance of the component as its argument. For example, if we wanted to wrap the CustomTextInput above to simulate it being clicked immediately after mounting:

> class AutoFocusTextInput extends React.Component {
  componentDidMount() {
    this.textInput.focus();
  }
  render() {
    return (
      <CustomTextInput
        ref={(input) = { this.textInput = input; }} /
    );
  }
}

Note that this only works if CustomTextInput is declared as a class:

class CustomTextInput extends React.Component {
  // ...
}

-You may not use the ref attribute on functional components because they don't have instances. You should convert the component to a class if you need a ref to it, just like you do when you need lifecycle methods or state.
You can, however, use the ref attribute inside a functional component as long as you refer to a DOM element or a class component:

-Your first inclination may be to use refs to "make things happen" in your app. If this is the case, take a moment and think more critically about where state should be owned in the component hierarchy. Often, it becomes clear that the proper place to "own" that state is at a higher level in the hierarchy.

-**If you worked with React before, you might be familiar with an older API where the ref attribute is a string, like "textInput", and the DOM node is accessed as this.refs.textInput. We advise against it because string refs have some issues, are considered legacy, and are likely to be removed in one of the future releases. If you're currently using this.refs.textInput to access refs, we recommend the callback pattern instead.**

### Uncontrolled Components

-In most cases, we recommend using controlled components to implement forms. In a controlled component, form data is handled by a React component. The alternative is uncontrolled components, where form data is handled by the DOM itself.
To write an uncontrolled component, instead of writing an event handler for every state update, you can use a ref to get form values from the DOM.

-In the React rendering lifecycle, the value attribute on form elements will override the value in the DOM. With an uncontrolled component, you often want React to specify the initial value, but leave subsequent updates uncontrolled. To handle this case, you can specify a defaultValue attribute instead of value.


### Optimizing Performance
Internally, React uses several clever techniques to minimize the number of costly DOM operations required to update the UI. For many applications, using React will lead to a fast user interface without doing much work to specifically optimize for performance. Nevertheless, there are several ways you can speed up your React application.

-If you're benchmarking or experiencing performance problems in your React apps, make sure you're testing with the minified production build:

React builds and maintains an internal representation of the rendered UI. It includes the React elements you return from your components. This representation lets React avoid creating DOM nodes and accessing existing ones beyond necessity, as that can be slower than operations on JavaScript objects. Sometimes it is referred to as a "virtual DOM", but it works the same way on React Native.

When a component's props or state change, React decides whether an actual DOM update is necessary by comparing the newly returned element with the previously rendered one. When they are not equal, React will update the DOM.

In some cases, your component can speed all of this up by overriding the lifecycle function shouldComponentUpdate, which is triggered before the re-rendering process starts. The default implementation of this function returns true, leaving React to perform the update:

> shouldComponentUpdate(nextProps, nextState) {
  return true;
}

If you know that in some situations your component doesn't need to update, you can return false from shouldComponentUpdate instead, to skip the whole rendering process, including calling render() on this component and below.

-The Power Of Not Mutating Data
The simplest way to avoid this problem is to avoid mutating values that you are using as props or state. For example, the handleClick method above could be rewritten using concat as:

> handleClick() {
  this.setState(prevState = ({
    words: prevState.words.concat(['marklar'])
  }));
}

ES6 supports a spread syntax for arrays which can make this easier. If you're using Create React App, this syntax is available by default.

> handleClick() {
  this.setState(prevState = ({
    words: [...prevState.words, 'marklar'],
  }));
};

You can also rewrite code that mutates objects to avoid mutation, in a similar way. For example, let's say we have an object named colormap and we want to write a function that changes colormap.right to be 'blue'. We could write:

> function updateColorMap(colormap) {
  colormap.right = 'blue';
}
To write this without mutating the original object, we can use Object.assign method:
function updateColorMap(colormap) {
  return Object.assign({}, colormap, {right: 'blue'});
}

updateColorMap now returns a new object, rather than mutating the old one. Object.assign is in ES6 and requires a polyfill.

There is a JavaScript proposal to add object spread properties to make it easier to update objects without mutation as well:

function updateColorMap(colormap) {
  return {...colormap, right: 'blue'};
}
If you're using Create React App, both Object.assign and the object spread syntax are available by default.

**Using Immutable Data Structures**
Immutable.js is another way to solve this problem. It provides immutable, persistent collections that work via structural sharing:

Immutable: once created, a collection cannot be altered at another point in time.
Persistent: new collections can be created from a previous collection and a mutation such as set. The original collection is still valid after the new collection is created.
Structural Sharing: new collections are created using as much of the same structure as the original collection as possible, reducing copying to a minimum to improve performance.
Immutability makes tracking changes cheap. A change will always result in a new object so we only need to check if the reference to the object has changed. 

Two other libraries that can help use immutable data are seamless-immutable and immutability-helper.
Immutable data structures provide you with a cheap way to track changes on objects, which is all we need to implement shouldComponentUpdate. This can often provide you with a nice performance boost.













