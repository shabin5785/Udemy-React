- Redux includes all the data or state of app. Not just data, the meta data as well. like current selection, preferences etc. React represents the views that translates the redux state to views. We centralize all the data of an app in single library. Redux so has application state. while react has component level state. SO redux advocates separation of state of app and react as the view layer

- Reducer is a function that returns a piece of appplication state. We can have many reducers as app can have many different state, like on reducer for list of books and one for current book Reducers produce the value of the state

-React-redux manages the state merge between react and redux. Redux state is sliced by a reducer (or the entire state if needed) and this is to be give to react to show in view. This part of merging or interaction is handled by react redux

- A container is a react component that has a direct relation with the state managed by redux. Container are the only bridge between react and redux. Continaers are sometimes called as Smart Components as opposed to normal dumb components. So which components in react needs to be promoted to containers?

- in general we want the most parent component taht cares about a number of other components to be a container.  BUt this is not always correct. main app may not always care about the state of app , will just render the app. so choose based on the component behaviour as well

- if a parent componet is conencted to redux and hence is a container, then the child components of that does not need to be connected to the redux. its by default connected through parent component

- in a contianer if the state passed ever changes, the container rerender.

- in backedn, redux generates a state object (using store), we add data to it using reducers and then link this to react to be displayed.

-action and action creators are responsible for changing the state

- an action creator is a fn that returns an action. This action has details about the action being generated. the action is then is automatically send to all reducers in the application. Reducer can choose depending on action a differnt state. This state gets pumped to app state,causing the app to rerender. All this is triggered by some action like user click or ajax request etc. For all this work we need to wire action creator to redux.

-bindactioncreators function helps in wiring action with redux
