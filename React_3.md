- A simple component if it has to talk to redux has to be a container. So make it a class as well.

- Controlled field is one with value being set by the state element.

- all event handler functions come around with the event object as argument

- inside a callback fn , this has not the current scope value (check this). this occurs when we just call the fn. THis can be avaoided by passing callback as fat arrow fn or binding this to the call back function.
this (aka "the context") is a special keyword inside each function and its value only depends on how the function was called, not how/when/where it was defined. It is not affected by lexical scope, like other variables. Here are some examples:

- Middlwares are fns that take an action, depending on action type or payload or any property, decide to let the action pass or modify it or stop it. before reaching the reducer. All actions in fact flow through the middlewares.

- WE can have any stage or steps of middlewares. All are linked through and actins pass through all middlewares before reaching reducer.

- redux middleware stops an action if action has a promise as payload. It resume it once promise returns


