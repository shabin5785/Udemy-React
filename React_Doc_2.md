### Lists and Keys

Map function in js is like this :Given the code below, we use the map() function to take an array of numbers and double their values. We assign the new array returned by map() to the variable doubled and log it:

> const numbers = [1, 2, 3, 4, 5];
const doubled = numbers.map((number) = number * 2);
console.log(doubled);
In React, transforming arrays into lists of elements is nearly identical.

You can build collections of elements and include them in JSX using curly braces {}.

Below, we loop through the numbers array using the Javascript map() function. We return an <li> element for each item. Finally, we assign the resulting array of elements to listItems:

> const numbers = [1, 2, 3, 4, 5];
const listItems = numbers.map((number) =
  <li{number}</li
);

We include the entire listItems array inside a <ul> element, and render it to the DOM:

> ReactDOM.render(
  <ul{listItems}</ul,
  document.getElementById('root')
);

Usually you would render lists inside a component.

We can refactor the previous example into a component that accepts an array of numbers and outputs an unordered list of elements.

> function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =
    <li{number}</li
  );
  return (
    <ul{listItems}</ul
  );
}

> const numbers = [1, 2, 3, 4, 5];
ReactDOM.render(
  <NumberList numbers={numbers} /,
  document.getElementById('root')
);


**Keys**
Keys help React identify which items have changed, are added, or are removed. Keys should be given to the elements inside the array to give the elements a stable identity:The best way to pick a key is to use a string that uniquely identifies a list item among its siblings. When you dont have stable IDs for rendered items, you may use the item index as a key as a last resort:

> const todoItems = todos.map((todo, index) =
  // Only do this if items have no stable IDs
  <li key={index}
    {todo.text}
  </li
);

Keys only make sense in the context of the surrounding array.

For example, if you extract a ListItem component, you should keep the key on the <ListItem /> elements in the array rather than on the root <li> element in the ListItem itself.

Example: Incorrect Key Usage

> function ListItem(props) {
  const value = props.value;
  return (
    // Wrong! There is no need to specify the key here:
    <li key={value.toString()}
      {value}
    </li
  );
}> We loved with a love that was more than love



function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    // Wrong! The key should have been specified here:
    <ListItem value={number} />
  );
  return (
    <ul>
      {listItems}
    </ul>
  );
}


> const listItems = numbers.map((number) =
    // Correct! Key should be specified inside the array.
    <ListItem key={number.toString()}
              value={number} /
  );
  
Keys used within arrays should be unique among their siblings. However they don't need to be globally unique. Keys serve as a hint to React but they don't get passed to your components. If you need the same value in your component, pass it explicitly as a prop with a different name:

> const content = posts.map((post) =
  <Post
    key={post.id}
    id={post.id}
    title={post.title} /
);

With the example above, the Post component can read props.id, but not props.key.

### Forms
HTML form elements work a little bit differently from other DOM elements in React, because form elements naturally keep some internal state
This form has the default HTML form behavior of browsing to a new page when the user submits the form. If you want this behavior in React, it just works. But in most cases, it's convenient to have a JavaScript function that handles the submission of the form and has access to the data that the user entered into the form. The standard way to achieve this is with a technique called "controlled components".

**Controlled Components**

In HTML, form elements such as <input>, <textarea>, and <select> typically maintain their own state and update it based on user input. In React, mutable state is typically kept in the state property of components, and only updated with setState().

We can combine the two by making the React state be the "single source of truth". Then the React component that renders a form also controls what happens in that form on subsequent user input. An input form element whose value is controlled by React in this way is called a "controlled component".

> class NameForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {value: ''};
    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }
  handleChange(event) {
    this.setState({value: event.target.value});
  }
  handleSubmit(event) {
    alert('A name was submitted: ' + this.state.value);
    event.preventDefault();
  }
	render() {
    return (
      <form onSubmit={this.handleSubmit}
        <label
          Name:
          <input type="text" value={this.state.value} onChange={this.handleChange} /
        </label
        <input type="submit" value="Submit" /
      </form
    );
  }
}

Since the value attribute is set on our form element, the displayed value will always be this.state.value, making the React state the source of truth. Since handleChange runs on every keystroke to update the React state, the displayed value will update as the user types.

With a controlled component, every state mutation will have an associated handler function. This makes it straightforward to modify or validate user input. 

In React, a <textarea> uses a value attribute instead. This way, a form using a <textarea> can be written very similarly to a form that uses a single-line input:

 React, instead of using this selected attribute, uses a value attribute on the root select tag. This is more convenient in a controlled component because you only need to update it in one place
 
 Overall, this makes it so that <input type="text">, <textarea>, and <select> all work very similarly - they all accept a value attribute that you can use to implement a controlled component.
 
 When you need to handle multiple controlled input elements, you can add a name attribute to each element and let the handler function choose what to do based on the value of event.target.name.
 
> handleInputChange(event) {
    const target = event.target;
    const value = target.type === 'checkbox' ? target.checked : target.value;
    const name = target.name;

    this.setState({
      [name]: value
    });
  }
  
### Lifting State Up
Often, several components need to reflect the same changing data. We recommend lifting the shared state up to their closest common ancestor. 

If we have a component and two objects or instances of that, then each will have a state of its own. No sync between them. To solve this, we put the state in common ancestor or parent of the component. The parent will then pass the state as props to child components. Now issue is child cannot update state as props are read only and state is in parent. So parent also passes a fn to update state to the child. In React, this is usually solved by making a component "controlled". Just like the DOM <input> accepts both a value and an onChange prop, 

In React, sharing state is accomplished by moving it up to the closest common ancestor of the components that need it. This is called "lifting state up". The parent holding the state becomes single source of truth.  It can instruct them both to have values that are consistent with each other.

Excellent example here https://facebook.github.io/react/docs/lifting-state-up.html

### Composition vs Inheritance
React has a powerful composition model, and we recommend using composition instead of inheritance to reuse code between components.

- Some components dont know their children ahead of time. This is especially common for components like Sidebar or Dialog that represent generic "boxes". We recommend that such components use the special children prop to pass children elements directly into their output:

> function FancyBorder(props) {
  return (
    <div className={'FancyBorder FancyBorder-' + props.color}
      {props.children}
    </div
  );
}

This lets other components pass arbitrary children to them by nesting the JSX:
> function WelcomeDialog() {
  return (
    <FancyBorder color="blue"
      <h1 className="Dialog-title"
        Welcome
      </h1
      <p className="Dialog-message"
        Thank you for visiting our spacecraft!
      </p
    </FancyBorder
  );
}

We can also add different keys to the passed data and in the side bar or menu, split and show them

**Specialization**
Sometimes we think about components as being "special cases" of other components. For example, we might say that a WelcomeDialog is a special case of Dialog.

In React, this is also achieved by composition, where a more "specific" component renders a more "generic" one and configures it with props:

> function Dialog(props) {
  return (
    <FancyBorder color="blue"
      <h1 className="Dialog-title"
        {props.title}
      </h1
      <p className="Dialog-message"
        {props.message}
      </p
    </FancyBorder
  );
}
function WelcomeDialog() {
  return (
    <Dialog
      title="Welcome"
      message="Thank you for visiting our spacecraft!" />
  );
}

One such technique is the single responsibility principle, that is, a component should ideally only do one thing. If it ends up growing, it should be decomposed into smaller subcomponents.

----------------------------------------

Let's go through each one and figure out which one is state. Simply ask three questions about each piece of data:

Is it passed in from a parent via props? If so, it probably isn't state.
Does it remain unchanged over time? If so, it probably isn't state.
Can you compute it based on any other state or props in your component? If so, it isn't state.
The original list of products is passed in as props, so that's not state. The search text and the checkbox seem to be state since they change over time and can't be computed from anything. And finally, the filtered list of products isn't state because it can be computed by combining the original list of products with the search text and value of the checkbox.

For each piece of state in your application:

Identify every component that renders something based on that state.
Find a common owner component (a single component above all the components that need the state in the hierarchy).
Either the common owner or another component higher up in the hierarchy should own the state.
If you can't find a component where it makes sense to own the state, create a new component simply for holding the state and add it somewhere in the hierarchy above the common owner component.

