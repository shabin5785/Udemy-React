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

