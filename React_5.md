- React -> user interacts and creates action -> action creator -> produces action -> flows into middleware -> passes action to reducers -> produces state-> state goes back to react -> cycle repeats

- Redux thunk is used to create async action calls.. Raect out of box doesnt support async calls. Redux thunk gives us control over the dispatch method. Dispatch method is part of redux store that contains our app state. Dispatch method handles all the steps for action once its creatged. Like flow to middleware, reducers etc. Thunk helps us to hack into this.

- In vanilla react, an action creator has to return an action syncronously ie, at end of method. even with axios we have to reutn the payload from action creator. here we return an action throgh thunk and by dispatch method. More like we pass a callback to dispatch, and after request or async operation the callback is invoked by thunk.

- Firebase? One think firebase causes events to be generated for delete, update , insert etc. So state changes is automaticaly triggered. We dont have to fetch data again after an event. Firebase is event based flow. So we subscribe to events and return actions async with thunk

- try to use helper methods and js libraries to avoid repetitive and large codes.. like repeat divs, validations, getting values from maps etc Html is just string so we can append strings, concat etc and create code within fns and loops and reduce code footprint
