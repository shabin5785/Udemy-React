- A simple component if it has to talk to redux has to be a container. So make it a class as well.

- Controlled field is one with value being set by the state element.

- all event handler functions come around with the event object as argument

- inside a callback fn , this has not the current scope value (check this). this occurs when we just call the fn. THis can be avaoided by passing callback as fat arrow fn or binding this to the call back function.
this (aka "the context") is a special keyword inside each function and its value only depends on how the function was called, not how/when/where it was defined. It is not affected by lexical scope, like other variables. Here are some examples:




