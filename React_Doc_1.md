- React components implement a render() method that takes input data and returns what to display. Input data that is passed into the component can be accessed by render() via this.props.

class HelloMessage extends React.Component {
  render() {
    return <divHello {this.props.name}</div;
  }
}

ReactDOM.render(<HelloMessage name="Jane" /, mountNode);

In addition to taking input data (accessed via this.props), a component can maintain internal state data (accessed via this.state). When a component's state data changes, the rendered markup will be updated by re-invoking render().> We loved with a love that was more than love



