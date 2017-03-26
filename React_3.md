- A simple component if it has to talk to redux has to be a container. So make it a class as well.

- Controlled field is one with value being set by the state element.

- all event handler functions come around with the event object as argument

- inside a callback fn , this has not the current scope value (check this). this occurs when we just call the fn. THis can be avaoided by passing callback as fat arrow fn or binding this to the call back function.
this (aka "the context") is a special keyword inside each function and its value only depends on how the function was called, not how/when/where it was defined. It is not affected by lexical scope, like other variables. Here are some examples:

- Middlwares are fns that take an action, depending on action type or payload or any property, decide to let the action pass or modify it or stop it. before reaching the reducer. All actions in fact flow through the middlewares.

- WE can have any stage or steps of middlewares. All are linked through and actins pass through all middlewares before reaching reducer.

- redux middleware stops an action if action has a promise as payload. It creates a new state with same type as old and activates that when promise returns. beauty of this is we avoid callback hell for async. Middleware takes care of this

- containers are always class based. Components can be class or functional

- ref property in react allows a component to get refernce to a rendered object in a page. So we can add ref to a component and later refer it using this.refs.<name> anyware in the project.

- normally to work with third party libraries that dont know how to render using react, like google maps( they know how to render themselves, but not in react context), we decalre a react component with a ref attribtue and then use that ref as reference to render the third party library.
