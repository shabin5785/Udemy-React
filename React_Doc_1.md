- React components implement a render() method that takes input data and returns what to display. Input data that is passed into the component can be accessed by render() via this.props.

> class HelloMessage extends React.Component {
  render() {
    return <divHello {this.props.name}</div;
  }
}

ReactDOM.render(<HelloMessage name="Jane" /, mountNode);
  
  

