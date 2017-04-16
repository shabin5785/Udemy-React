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
