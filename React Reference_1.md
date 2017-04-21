-React.PureComponent is exactly like React.Component but implements shouldComponentUpdate() with a shallow prop and state comparison.If your React component's render() function renders the same result given the same props and state, you can use React.PureComponent for a performance boost in some cases.
React.PureComponent's shouldComponentUpdate() only shallowly compares the objects. If these contain complex data structures, it may produce false-negatives for deeper differences. Only extend PureComponent when you expect to have simple props and state, or use forceUpdate() when you know deep data structures have changed. Or, consider using immutable objects to facilitate fast comparisons of nested data.
Furthermore, React.PureComponent's shouldComponentUpdate() skips prop updates for the  whole component subtree. Make sure all the children components are also "pure".

-cloneElement() : Clone and return a new React element using element as the starting point. The resulting element will have the original element's props with the new props merged in shallowly. New children will replace existing children. key and ref from the original element will be preserved. However, it also preserves refs. This means that if you get a child with a ref on it, you won't accidentally steal it from your ancestor. You will get the same ref attached to your new element.

-createFactory(): Return a function that produces React elements of a given type. Like React.createElement(), the type argument can be either a tag name string (such as 'div' or 'span'), or a React component type (a class or a function).This helper is considered legacy, and we encourage you to either use JSX or use React.createElement() directly instead.

-React.Children provides utilities for dealing with the this.props.children opaque data structure. React.Children.map
Invokes a function on every immediate child contained within children with this set to thisArg. If children is a keyed fragment or array it will be traversed: the function will never be passed the container objects. If children is null or undefined, returns null or undefined rather than an array.
React.Children.forEach is like map above but does not return array

-React.Component is an abstract base class, so it rarely makes sense to refer to React.Component directly. Instead, you will typically subclass it, and define at least a render() method.

**The Component Lifecycle**
Each component has several "lifecycle methods" that you can override to run code at particular times in the process. Methods prefixed with will are called right before something happens, and methods prefixed with did are called right after something happens.

Mounting
These methods are called when an instance of a component is being created and inserted into the DOM:

> constructor()
componentWillMount()
render()
componentDidMount()
Updating

An update can be caused by changes to props or state. These methods are called when a component is being re-rendered:

> componentWillReceiveProps()
shouldComponentUpdate()
componentWillUpdate()
render()
componentDidUpdate()

Unmounting
This method is called when a component is being removed from the DOM:

> componentWillUnmount()

- The render() method is required.

When called, it should examine this.props and this.state and return a single React element. This element can be either a representation of a native DOM component, such as <div />, or another composite component that you've defined yourself.
You can also return null or false to indicate that you don't want anything rendered. When returning null or false, ReactDOM.findDOMNode(this) will return null.
The render() function should be pure, meaning that it does not modify component state, it returns the same result each time it's invoked, and it does not directly interact with the browser. If you need to interact with the browser, perform your work in componentDidMount() or the other lifecycle methods instead. Keeping render() pure makes components easier to think about.

-The constructor for a React component is called before it is mounted. When implementing the constructor for a React.Component subclass, you should call super(props) before any other statement. Otherwise, this.props will be undefined in the constructor, which can lead to bugs.
The constructor is the right place to initialize state. If you don't initialize state and you don't bind methods, you don't need to implement a constructor for your React component.It's okay to initialize state based on props. This effectively "forks" the props and sets the state with the initial props.

-setState() enqueues changes to the component state and tells React that this component and its children need to be re-rendered with the updated state. This is the primary method you use to update the user interface in response to event handlers and server responses.
Think of setState() as a request rather than an immediate command to update the component. For better perceived performance, React may delay it, and then update several components in a single pass. React does not guarantee that the state changes are applied immediately.

setState() does not always immediately update the component. It may batch or defer the update until later. This makes reading this.state right after calling setState() a potential pitfall. Instead, use componentDidUpdate or a setState callback (setState(updater, callback)), either of which are guaranteed to fire after the update has been applied.

setState() will always lead to a re-render unless shouldComponentUpdate() returns false. If mutable objects are being used and conditional rendering logic cannot be implemented in shouldComponentUpdate(), calling setState() only when the new state differs from the previous state will avoid unnecessary re-renders.

The first argument is an updater function with the signature:

> (prevState, props) = nextState

prevState is a reference to the previous state. It should not be directly mutated. Instead, changes should be represented by building a new state object based on the input from prevState and props. 
Both prevState and props received by the updater function are guaranteed to be up-to-date.
The second parameter to setState() is an optional callback function that will be executed once setState is completed and the component is re-rendered. Generally we recommend using componentDidUpdate() for such logic instead.

**Class Properties**
defaultProps can be defined as a property on the component class itself, to set the default props for the class. This is used for undefined props, but not for null props.

**Instance Properties**
this.props contains the props that were defined by the caller of this component. See Components and Props for an introduction to props.In particular, this.props.children is a special prop, typically defined by the child tags in the JSX expression rather than in the tag itself.

The state contains data specific to this component that may change over time. The state is user-defined, and it should be a plain JavaScript object.If you don't use it in render(), it shouldn't be on the state. For example, you can put timer IDs directly on the instance.Never mutate this.state directly, as calling setState() afterwards may replace the mutation you made. Treat this.state as if it were immutable.

- render(): Render a React element into the DOM in the supplied container and return a reference to the component (or returns null for stateless components).If the React element was previously rendered into container, this will perform an update on it and only mutate the DOM as necessary to reflect the latest React element.If the optional callback is provided, it will be executed after the component is rendered or updated.

-React implements a browser-independent DOM system for performance and cross-browser compatibility. In React, all DOM properties and attributes (including event handlers) should be camelCased. For example, the HTML attribute tabindex corresponds to the attribute tabIndex in React. 

-The checked attribute is supported by <input> components of type checkbox or radio. You can use it to set whether the component is checked. To specify a CSS class, use the className attribute. This applies to all regular DOM and SVG elements like <div>, <a>, and others. 

dangerouslySetInnerHTML is React's replacement for using innerHTML in the browser DOM. In general, setting HTML from code is risky because it's easy to inadvertently expose your users to a cross-site scripting (XSS) attack. So, you can set HTML directly from React, but you have to type out dangerouslySetInnerHTML and pass an object with a __html key, to remind yourself that it's dangerous







