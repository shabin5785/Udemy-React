### Actions
-Actions are payloads of information that send data from your application to your store. They are the only source of information for the store. You send them to the store using store.dispatch().Actions are plain JavaScript objects. Actions must have a type property that indicates the type of action being performed. Types should typically be defined as string constants. Once your app is large enough, you may want to move them into a separate module.
Other than type, the structure of an action object is really up to you.

- Action creators are exactly that—functions that create actions.In Redux action creators simply return an action:

> function addTodo(text) {
  return {
    type: ADD_TODO,
    text
  }
}

This makes them portable and easy to test.

### Reducers
- Actions describe the fact that something happened, but don't specify how the application's state changes in response. This is the job of reducers.
In Redux, all the application state is stored as a single object. It's a good idea to think of its shape before writing any code.

The reducer is a pure function that takes the previous state and an action, and returns the next state.
(previousState, action) => newState

It's called a reducer because it's the type of function you would pass to Array.prototype.reduce(reducer, ?initialValue). It's very important that the reducer stays pure. Things you should never do inside a reducer:

Mutate its arguments;
Perform side effects like API calls and routing transitions;
Call non-pure functions, e.g. Date.now() or Math.random().

### Store

In the previous sections, we defined the actions that represent the facts about “what happened” and the reducers that update the state according to those actions.

The Store is the object that brings them together. The store has the following responsibilities:

- Holds application state;
- Allows access to state via getState();
- Allows state to be updated via dispatch(action);
- Registers listeners via subscribe(listener);
- Handles unregistering of listeners via the function returned by subscribe(listener)

It's important to note that you'll only have a single store in a Redux application. When you want to split your data handling logic, you'll use reducer composition instead of many stores.

### Data Flow
Redux architecture revolves around a strict unidirectional data flow.
This means that all data in an application follows the same lifecycle pattern, making the logic of your app more predictable and easier to understand. It also encourages data normalization, so that you don't end up with multiple, independent copies of the same data that are unaware of one another.

The data lifecycle in any Redux app follows these 4 steps:
1. You call store.dispatch(action).
An action is a plain object describing what happened.You can call store.dispatch(action) from anywhere in your app, including components and XHR callbacks, or even at scheduled intervals.

2.The Redux store calls the reducer function you gave it.The store will pass two arguments to the reducer: the current state tree and the action.Note that a reducer is a pure function. It only computes the next state. It should be completely predictable: calling it with the same inputs many times should produce the same outputs. It shouldn't perform any side effects like API calls or router transitions. These should happen before an action is dispatched.

3. The root reducer may combine the output of multiple reducers into a single state tree.How you structure the root reducer is completely up to you. Redux ships with a combineReducers() helper function, useful for “splitting” the root reducer into separate functions that each manage one branch of the state tree.

4. The Redux store saves the complete state tree returned by the root reducer.This new tree is now the next state of your app! Every listener registered with store.subscribe(listener) will now be invoked; listeners may call store.getState() to get the current state.

### Usage with React
Redux has no relation to React. You can write Redux apps with React, Angular, Ember, jQuery, or vanilla JavaScript.
That said, Redux works especially well with libraries like React and Deku because they let you describe UI as a function of state, and Redux emits state updates in response to actions.











