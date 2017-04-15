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

Typically, new React apps have a single App component at the very top. However, if you integrate React into an existing app, you might start bottom-up with a small component like Button and gradually work your way to the top of the view hierarchy. Components must return a single root element. This is why we added a <div> to contain all the <Welcome /> elements.

- Don't be afraid to split components into smaller components. Extracting components might seem like grunt work at first, but having a palette of reusable components pays off in larger apps. A good rule of thumb is that if a part of your UI is used several times (Button, Panel, Avatar), or is complex enough on its own (App, FeedStory, Comment), it is a good candidate to be a reusable component.

Whether you declare a component as a function or a class, it must never modify its own props. Consider this sum function:

function sum(a, b) {
  return a + b;
}
Such functions are called "pure" because they do not attempt to change their inputs, and always return the same result for the same inputs.

In contrast, this function is impure because it changes its own input:

function withdraw(account, amount) {
  account.total -= amount;
}
React is pretty flexible but it has a single strict rule:

All React components must act like pure functions with respect to their props.

Of course, application UIs are dynamic and change over time. In the next section, we will introduce a new concept of "state". State allows React components to change their output over time in response to user actions, network responses, and anything else, without violating this rule.

-State is similar to props, but it is private and fully controlled by the component.
We mentioned before that components defined as classes have some additional features. Local state is exactly that: a feature available only to classes.

You can convert a functional component like Clock to a class in five steps:

Create an ES6 class with the same name that extends React.Component.

Add a single empty method to it called render().

Move the body of the function into the render() method.

Replace props with this.props in the render() body.

Delete the remaining empty function declaration.

> class Clock extends React.Component {
  render() {
    return (
      <div
        <h1Hello, world!</h1
        <h2It is {this.props.date.toLocaleTimeString()}.</h2
      </div
    );
  }
}
ReactDOM.render(
  <Clock /,
  document.getElementById('root')
);

### Adding Local State to a Class
- Replace this.props.date with this.state.date in the render() method:
- Add a class constructor that assigns the initial this.state:Class components should always call the base constructor with props.
- No need to pass props while using the component now.

> class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }
render() {
    return (
      <div
        <h1Hello, world!</h1
        <h2It is {this.state.date.toLocaleTimeString()}.</h2
      </div
    );
  }
}
ReactDOM.render(
  <Clock /,
  document.getElementById('root')
);

### Adding Lifecycle Methods to a Class
- We can declare special methods on the component class to run some code when a component mounts and unmounts:
> componentDidMount() {

  }

  componentWillUnmount() {

  }
  
  These methods are called "lifecycle hooks".The componentDidMount() hook runs after the component output has been rendered to the DOM. 
  
 - While this.props is set up by React itself and this.state has a special meaning, you are free to add additional fields to the class manually if you need to store something that is not used for the visual output.
If you don't use something in render(), it shouldn't be in the state.

> class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }
componentDidMount() {
    this.timerID = setInterval(
      () = this.tick(),
      1000
    );
  }
componentWillUnmount() {
    clearInterval(this.timerID);
  }
tick() {
    this.setState({
      date: new Date()
    });
  }
render() {
    return (
      <div
        <h1Hello, world!</h1
        <h2It is {this.state.date.toLocaleTimeString()}.</h2
      </div
    );
  }
}


1) When <Clock /> is passed to ReactDOM.render(), React calls the constructor of the Clock component. Since Clock needs to display the current time, it initializes this.state with an object including the current time. We will later update this state.

2) React then calls the Clock component's render() method. This is how React learns what should be displayed on the screen. React then updates the DOM to match the Clock's render output.

3) When the Clock output is inserted in the DOM, React calls the componentDidMount() lifecycle hook. Inside it, the Clock component asks the browser to set up a timer to call tick() once a second.

4) Every second the browser calls the tick() method. Inside it, the Clock component schedules a UI update by calling setState() with an object containing the current time. Thanks to the setState() call, React knows the state has changed, and calls render() method again to learn what should be on the screen. This time, this.state.date in the render() method will be different, and so the render output will include the updated time. React updates the DOM accordingly.

5) If the Clock component is ever removed from the DOM, React calls the componentWillUnmount() lifecycle hook so the timer is stopped.

### Using State Correctly

**Do Not Modify State Directly**
For example, this will not re-render a component:

> // Wrong
this.state.comment = 'Hello';
Instead, use setState():
// Correct
this.setState({comment: 'Hello'});

The only place where you can assign this.state is the constructor.

****State Updates May Be Asynchronous
React may batch multiple setState() calls into a single update for performance.

Because this.props and this.state may be updated asynchronously, you should not rely on their values for calculating the next state.

For example, this code may fail to update the counter:

> // Wrong
this.setState({
  counter: this.state.counter + this.props.increment,
});

To fix it, use a second form of setState() that accepts a function rather than an object. That function will receive the previous state as the first argument, and the props at the time the update is applied as the second argument:

> // Correct
this.setState((prevState, props) = ({
  counter: prevState.counter + props.increment
}));

****State Updates are Merged
When you call setState(), React merges the object you provide into the current state.

For example, your state may contain several independent variables:

 > constructor(props) {
    super(props);
    this.state = {
      posts: [],
      comments: []
    };
  }
  
Then you can update them independently with separate setState() calls:

The merging is shallow, so this.setState({comments}) leaves this.state.posts intact, but completely replaces this.state.comments.

### The Data Flows Down

Neither parent nor child components can know if a certain component is stateful or stateless, and they shouldn't care whether it is defined as a function or a class.

This is why state is often called local or encapsulated. It is not accessible to any component other than the one that owns and sets it.

A component may choose to pass its state down as props to its child components:

<h2>It is {this.state.date.toLocaleTimeString()}.</h2>
This also works for user-defined components:

<FormattedDate date={this.state.date} />
The FormattedDate component would receive the date in its props and wouldn't know whether it came from the Clock's state, from the Clock's props, or was typed by hand:

> function FormattedDate(props) {
  return <h2It is {props.date.toLocaleTimeString()}.</h2;
}

- This is commonly called a "top-down" or "unidirectional" data flow. Any state is always owned by some specific component, and any data or UI derived from that state can only affect components "below" them in the tree.

If you imagine a component tree as a waterfall of props, each component's state is like an additional water source that joins it at an arbitrary point but also flows down. In React apps, whether a component is stateful or stateless is considered an implementation detail of the component that may change over time. You can use stateless components inside stateful components, and vice versa.

### Handling Events

Handling events with React elements is very similar to handling events on DOM elements. There are some syntactic differences:

React events are named using camelCase, rather than lowercase.
With JSX you pass a function as the event handler, rather than a string.
For example, the HTML:

> <button onclick="activateLasers()"
  Activate Lasers
  </button>
  
is slightly different in React:

> <button onClick={activateLasers}
  Activate Lasers
  </button>

- Another difference is that you cannot return false to prevent default behavior in React. You must call preventDefault explicitly.

> function ActionLink() {
  function handleClick(e) {
    e.preventDefault();
    console.log('The link was clicked.');
  }
return (
    <a href="#" onClick={handleClick}
      Click me
    </a
  );
}

Here, e is a synthetic event. React defines these synthetic events according to the W3C spec, so you don't need to worry about cross-browser compatibility. 

- When using React you should generally not need to call addEventListener to add listeners to a DOM element after it is created. Instead, just provide a listener when the element is initially rendered.

When you define a component using an ES6 class, a common pattern is for an event handler to be a method on the class. For example, this Toggle component renders a button that lets the user toggle between "ON" and "OFF" states:

> class Toggle extends React.Component {
  constructor(props) {
    super(props);
    this.state = {isToggleOn: true};

    // This binding is necessary to make `this` work in the callback
    this.handleClick = this.handleClick.bind(this);
  }
handleClick() {
    this.setState(prevState = ({
      isToggleOn: !prevState.isToggleOn
    }));
  }
render() {
    return (
      <button onClick={this.handleClick}
        {this.state.isToggleOn ? 'ON' : 'OFF'}
      </button
    );
  }
}
ReactDOM.render(
  <Toggle /,
  document.getElementById('root')
);

**This in callback**
You have to be careful about the meaning of this in JSX callbacks. In JavaScript, class methods are not bound by default. If you forget to bind this.handleClick and pass it to onClick, this will be undefined when the function is actually called.

This is not React-specific behavior; it is a part of how functions work in JavaScript. Generally, if you refer to a method without () after it, such as onClick={this.handleClick}, you should bind that method.

If calling bind annoys you, there are two ways you can get around this. If you are using the experimental property initializer syntax, you can use property initializers to correctly bind callbacks:

> class LoggingButton extends React.Component {
  // This syntax ensures `this` is bound within handleClick.
  // Warning: this is *experimental* syntax.
  handleClick = () = {
    console.log('this is:', this);
  }
render() {
    return (
      <button onClick={this.handleClick}
        Click me
      </button
    );
  }
}

This syntax is enabled by default in Create React App.

If you aren't using property initializer syntax, you can use an arrow function in the callback:

> class LoggingButton extends React.Component {
  handleClick() {
    console.log('this is:', this);
  }
render() {
    // This syntax ensures `this` is bound within handleClick
    return (
      <button onClick={(e) = this.handleClick(e)}
        Click me
      </button
    );
  }
}

The problem with this syntax is that a different callback is created each time the LoggingButton renders. In most cases, this is fine. However, if this callback is passed as a prop to lower components, those components might do an extra re-rendering. We generally recommend binding in the constructor or using the property initializer syntax, to avoid this sort of performance problem.


### Conditional Rendering

In React, you can create distinct components that encapsulate behavior you need. Then, you can render only some of them, depending on the state of your application.

Conditional rendering in React works the same way conditions work in JavaScript. Use JavaScript operators like if or the conditional operator to create elements representing the current state, and let React update the UI to match them.

function UserGreeting(props) {
  return <h1>Welcome back!</h1>;
}

function GuestGreeting(props) {
  return <h1>Please sign up.</h1>;
}
We'll create a Greeting component that displays either of these components depending on whether a user is logged in:

> function Greeting(props) {
  const isLoggedIn = props.isLoggedIn;
  if (isLoggedIn) {
    return <UserGreeting /;
  }
  return <GuestGreeting /;
}
ReactDOM.render(
  // Try changing to isLoggedIn={true}:
  <Greeting isLoggedIn={false} /,
  document.getElementById('root')
);

**Element Variables**
You can use variables to store elements. This can help you conditionally render a part of the component while the rest of the output doesn't change.

> function LoginButton(props) {
  return (
    <button onClick={props.onClick}
      Login
    </button
  );
}
function LogoutButton(props) {
  return (
    <button onClick={props.onClick}
      Logout
    </button
  );
}

In the example below, we will create a stateful component called LoginControl.
It will render either <LoginButton /> or <LogoutButton /> depending on its current state.

> class LoginControl extends React.Component {
  constructor(props) {
    super(props);
    this.handleLoginClick = this.handleLoginClick.bind(this);
    this.handleLogoutClick = this.handleLogoutClick.bind(this);
    this.state = {isLoggedIn: false};
  }

> handleLoginClick() {
    this.setState({isLoggedIn: true});
  }

> handleLogoutClick() {
    this.setState({isLoggedIn: false});
  }
  render() {
    const isLoggedIn = this.state.isLoggedIn;
	 let button = null;
    if (isLoggedIn) {
      button = <LogoutButton onClick={this.handleLogoutClick} /;
    } else {
      button = <LoginButton onClick={this.handleLoginClick} /;
    }
return (
      <div
        <Greeting isLoggedIn={isLoggedIn} /
        {button}
      </div
    );
  }
}
ReactDOM.render(
  <LoginControl /,
  document.getElementById('root')
);

While declaring a variable and using an if statement is a fine way to conditionally render a component, sometimes you might want to use a shorter syntax. There are a few ways to inline conditions in JSX

**Inline If with Logical && Operator**

You may embed any expressions in JSX by wrapping them in curly braces. This includes the JavaScript logical && operator. It can be handy for conditionally including an element:

> function Mailbox(props) {
  const unreadMessages = props.unreadMessages;
  return (
    <div
      <h1Hello!</h1
      {unreadMessages.length  0 &&
        <h2
          You have {unreadMessages.length} unread messages.
        </h2
      }
    </div
  );
}

> const messages = ['React', 'Re: React', 'Re:Re: React'];
ReactDOM.render(
  <Mailbox unreadMessages={messages} /,
  document.getElementById('root')
);

It works because in JavaScript, true && expression always evaluates to expression, and false && expression always evaluates to false.

Therefore, if the condition is true, the element right after && will appear in the output. If it is false, React will ignore and skip it.

Another method for conditionally rendering elements inline is to use the JavaScript conditional operator condition ? true : false.

In the example below, we use it to conditionally render a small block of text.

> render() {
  const isLoggedIn = this.state.isLoggedIn;
  return (
    <div
      The user is <b{isLoggedIn ? 'currently' : 'not'}</b logged in.
    </div
  );
}

It can also be used for larger expressions although it is less obvious what's going on:

> render() {
  const isLoggedIn = this.state.isLoggedIn;
  return (
    <div
      {isLoggedIn ? (
        <LogoutButton onClick={this.handleLogoutClick} /
      ) : (
        <LoginButton onClick={this.handleLoginClick} /
      )}
    </div
  );
}

**Preventing Component from Rendering**
In rare cases you might want a component to hide itself even though it was rendered by another component. To do this return null instead of its render output.

In the example below, the <WarningBanner /> is rendered depending on the value of the prop called warn. If the value of the prop is false, then the component does not render:

function WarningBanner(props) {
  if (!props.warn) {
    return null;
  }

- Returning null from a component's render method does not affect the firing of the component's lifecycle methods. For instance, componentWillUpdate and componentDidUpdate will still be called.



