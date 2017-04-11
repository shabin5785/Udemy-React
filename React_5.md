- React -> user interacts and creates action -> action creator -> produces action -> flows into middleware -> passes action to reducers -> produces state-> state goes back to react -> cycle repeats

- Redux thunk is used to create async action calls.. Raect out of box doesnt support async calls. Redux thunk gives us control over the dispatch method. Dispatch method is part of redux store that contains our app state. Dispatch method handles all the steps for action once its creatged. Like flow to middleware, reducers etc. Thunk helps us to hack into this.

- In vanilla react, an action creator has to return an action syncronously ie, at end of method. even with axios we have to reutn the payload from action creator. here we return an action throgh thunk and by dispatch method. More like we pass a callback to dispatch, and after request or async operation the callback is invoked by thunk.

- Firebase? One think firebase causes events to be generated for delete, update , insert etc. So state changes is automaticaly triggered. We dont have to fetch data again after an event. Firebase is event based flow. So we subscribe to events and return actions async with thunk

- try to use helper methods and js libraries to avoid repetitive and large codes.. like repeat divs, validations, getting values from maps etc Html is just string so we can append strings, concat etc and create code within fns and loops and reduce code footprint

- reselect is used to calculate derived state. Example  we have some posts and need to show selectd posts from them. SO we have a state of posts plus selected. So final state is sum of two reducers, one for all posts and one for selected posts. Reselect can be used to derive at this calculated state.

- Isse with a plain react approach is that to find selected posts we need to knw the structure of all posts collection.  Reselcet provides a selector, that can take the two reducers output and give us our state . With each reducer nt knowing any idea abt internal state. We hand over state creation of reselecct, instead of doing it within reducer. So any where we want the final state to be a derived one from multiple states, we can use reselect

- instead of loading data on componentmount, we can load on route enter as well. more reusable. So not tied to any component. 

- Raectcsstransitiongroup is a component in react. It can be used to animate components or items.WE can add animations like fade, slide in etc. we can wrap our state cahnge liek add, delete etc in reactcsstxngrp and get animation. WE can style animation ourselves

- Four common errors, first: Forgetting to export from components leading to error like component should not be null or number etc. Second: wrong import, with and wihtout curly braces.. Third: Error in asycn calls or promises. and not catching or handling them.Fourth: React wont render js objects. So while returing or rendering data, use arrays or parse objects befre rendering

- MOdal is the pop up window with information. Slightly chalenging to do in react. 

- Storing state data as object is better instead of as array. First of all, in an array we have to iterate and find, while object we can use the key to find it easily. Also its easier to update object based state than array based. lodash method can convert an array to object.

- if we git a route and if no default file is configured, index.html will be served by the server. COmmon internet rule

- wihtout browser history, when we access links, the url changes but no new request is made to sever. This request is made only when page refreshes. We can overcome a single page app, whihc always serves the main page and then react components within that based on react routes.
