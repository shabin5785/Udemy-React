- React components implement a render() method that takes input data and returns what to display. Input data that is passed into the component can be accessed by render() via this.props.

> class HelloMessage extends React.Component {
  render() {
    return <div> Hello {this.props.name}</div;
  }
}

ReactDOM.render(<HelloMessage name="Jane" /, mountNode);

In addition to taking input data (accessed via this.props), a component can maintain internal state data (accessed via this.state). When a component's state data changes, the rendered markup will be updated by re-invoking render().> We loved with a love that was more than love

- JSX is a syntax extension to JavaScript. JSX produces React "elements". You can embed any JavaScript expression in JSX by wrapping it in curly braces.We split JSX over multiple lines for readability. While it isn't required, when doing this, we also recommend wrapping it in parentheses to avoid the pitfalls of automatic semicolon insertion. After compilation, JSX expressions become regular JavaScript objects.
This means that you can use JSX inside of if statements and for loops, assign it to variables, accept it as arguments, and return it from functions:

- You may use quotes to specify string literals as attributes:

const element = <div tabIndex="0"></div>;
You may also use curly braces to embed a JavaScript expression in an attribute:

const element = <img src={user.avatarUrl}></img>;
Don't put quotes around curly braces when embedding a JavaScript expression in an attribute. Otherwise JSX will treat the attribute as a string literal rather than an expression. You should either use quotes (for string values) or curly braces (for expressions), but not both in the same attribute.

-Since JSX is closer to JavaScript than HTML, React DOM uses camelCase property naming convention instead of HTML attribute names. For example, class becomes className in JSX, and tabindex becomes tabIndex

-It is safe to embed user input in JSX:

> const title = response.potentiallyMaliciousInput;
// This is safe:
const element = <h1{title}</h1;

By default, React DOM escapes any values embedded in JSX before rendering them. Thus it ensures that you can never inject anything that's not explicitly written in your application. Everything is converted to a string before being rendered. This helps prevent XSS (cross-site-scripting) attacks.

- Babel compiles JSX down to React.createElement() calls.

These two examples are identical:

> const element = (
  <h1 className="greeting"
    Hello, world!
  </h1
);

> const element = React.createElement(
  'h1',
  {className: 'greeting'},
  'Hello, world!'
);

React.createElement() performs a few checks to help you write bug-free code but essentially it creates an object like this:

> // Note: this structure is simplified
const element = {
  type: 'h1',
  props: {
    className: 'greeting',
    children: 'Hello, world'
  }
};

These objects are called "React elements". You can think of them as descriptions of what you want to see on the screen. React reads these objects and uses them to construct the DOM and keep it up to date.

- Elements are the smallest building blocks of React apps.

An element describes what you want to see on the screen:

> const element = <h1Hello, world</h1;

Unlike browser DOM elements, React elements are plain objects, and are cheap to create. React DOM takes care of updating the DOM to match the React elements.


- To render a React element into a root DOM node, pass both to ReactDOM.render():
<div id="root"></div>

> const element = <h1Hello, world</h1;
ReactDOM.render(
  element,
  document.getElementById('root')
);

- React elements are immutable. Once you create an element, you can't change its children or attributes. An element is like a single frame in a movie: it represents the UI at a certain point in time.
React DOM compares the element and its children to the previous one, and only applies the DOM updates necessary to bring the DOM to the desired state.Even though we create an element describing the whole UI tree on every tick, only the text node whose contents has changed gets updated by React DOM.


### Components and Props
Components let you split the UI into independent, reusable pieces, and think about each piece in isolation.
Conceptually, components are like JavaScript functions. They accept arbitrary inputs (called "props") and return React elements describing what should appear on the screen.

### Functional and Class Components
The simplest way to define a component is to write a JavaScript function:

> function Welcome(props) {
  return <h1Hello, {props.name}</h1;
}

This function is a valid React component because it accepts a single "props" object argument with data and returns a React element. We call such components "functional" because they are literally JavaScript functions.

You can also use an ES6 class to define a component:

> class Welcome extends React.Component {
  render() {
    return <h1Hello, {this.props.name}</h1;
  }
}

The above two components are equivalent from React's point of view.

### Rendering a Component
Previously, we only encountered React elements that represent DOM tags:

const element = <div />;
However, elements can also represent user-defined components:

const element = <Welcome name="Sara" />;
When React sees an element representing a user-defined component, it passes JSX attributes to this component as a single object. We call this object "props".

For example, this code renders "Hello, Sara" on the page:

> function Welcome(props) {
  return <h1Hello, {props.name}</h1;
}

const element = <Welcome name="Sara" /;
ReactDOM.render(
  element,
  document.getElementById('root')
);

Lets recap what happens in this example:

- We call ReactDOM.render() with the <Welcome name="Sara" /> element.
- React calls the Welcome component with {name: 'Sara'} as the props.
- Our Welcome component returns a <h1>Hello, Sara</h1> element as the result.
- React DOM efficiently updates the DOM to match <h1>Hello, Sara</h1>.

Always start component names with a capital letter.
For example, <div /> represents a DOM tag, but <Welcome /> represents a component and requires Welcome to be in scope.

### Composing Components

Components can refer to other components in their output. This lets us use the same component abstraction for any level of detail. A button, a form, a dialog, a screen: in React apps, all those are commonly expressed as components.

For example, we can create an App component that renders Welcome many times:

> function Welcome(props) {
  return <h1Hello, {props.name}</h1;
}
function App() {
  return (
    <div
      <Welcome name="Sara" /
      <Welcome name="Cahal" /
      <Welcome name="Edite" /
    </div
  );
}
ReactDOM.render(
  <App /,
  document.getElementById('root')
);

