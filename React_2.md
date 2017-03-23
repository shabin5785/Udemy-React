- Dowwards data flow means only the most parent component should be response for fetching data. So the main component that contains all other components

- {video: video} here key and value are same string. So ES6 we can write like {video}

- In react use className for referncing css class. Using class has conflicts with keyword class

- pass value to components using properties in jsx tag.. like props in html tags.. color, size width etc

- fn based, props are passed as arguments. In class based, props are avaialbel in any method as this.props. passing data is same in both cases

- map is the best way to iterate

- its better to use key value pairs as updates of specific items is easier. So preferably always add a key attribute..

-ES6 use tilde in strings for string interpolation instead of singel quote

-during intial load of app, the variables have no value. But still the components try to render them. This causes error. So we need to hanlde the null values or props. Some parent components cannot fetch data fast enough before the child is rendered. .Like fetching youtube videos.. this leads to above error.

- we need to put the functions taht update state in main file. .and pass it to the components. .The components in turn call the passed function. This is rarely more than two levels deep. Like passing callback functions to one component, to its child and like that. This is also confusing as we need to see multiple files to see wher the function is actually used. We have better approaches to this.

- lodash debounce can only allow a function to be called after a certain time.

- State can be component level state. First example, App has one state, search bar has another. .Redux has single state. React has component level state.

- action usually has a type and payload. TYpe descibes the action, every action must have a type that should descibe it. Action will be sent to all teh reducers by react redux wiring 

- all reducers get two arguments. current state and the action. So reducers are only ever caled when an action occurs. THe state is not the application state, but only the state the reducer is responsible for. THat state here is acytally the one produced by the reducer. This is sent back to it when an action occurs. 

> export default function(state, action) {
  state += 1
}

Here every time action occurs, state is incremented by one..as same state is passed back to it.

- every reducer needs to take care of action it doesnt care about,so that it pass the state through it

- react doesnt allow to return undefined state. So initialize state to null or empty obj before returning. But for null beware of using it during first call..  Bypass it by returnig empty object or doing a null check before using it

- never mutate state inside action. Return a clean state.. ie, slice or return whole state. .dont change it

- Component state is completely different from application state. no relation between them

- action invokes reducers and there by cause reducers to return different state based on action . this causes the app state to change , and components to re render. Here action is created by action creators that are plain js fns, which gets called from components resulting in actions.