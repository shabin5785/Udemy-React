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

- 
