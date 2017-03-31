- react router also has a tiny package within it called history, that handles all url links and histories. History library watches for url changes and then indicates it to react router. react router depending on url changes updates the react component that needs to be displayed on scren and pass it to react.. React inturn render the new components.

- browserhistory library takes everyting after the protocol part. This is not the history library above. We can also use hashHistory, anything after hash be used for tracking. Memory history doesnt use the url at all.. We can use any three of these. All these three tell react route the chane in url or page.

- while using routes, we remove the main app from index.js or main page, and server the routes from index.js. Through routes we map root url to APp or main component

- Nesting routes.
> <Route path="/" component={App} 
  <Route path="g1" component={Greeting} /
  <Route path="g2" component={Greeting} /
</Route

Issue above is route know we want to show App and Greeting for path /g1. But it doesnt know where to put greeting and App. App and Greeting have parent child relationship. We need to tell APp to show the children. We can do that using   {this.props.children}. All child components are passed to App as child in props. Where we put the   {this.props.children} line in App decides where to put the children. In which div, etc.

- IndexRoute is a helper that behaves that behaves like a route. It activates when a route is matched with one defined by the parent but  not the children. Useful in below case.
We want our root "/" to show one basic component. But our desing demands we show the welcome contest as well for "/". Changing "/" to Welcome content is not good practice. Keep "/" to basic component. we can use indexcomponent to help us here.

- Redux promise library unravels the promises returned by apis.

- the react can flow can be triggered by a number of scenarions .Like hitting serach button or loading home page etc. For cases with no specific input , like loading home page, we can trigger base action in life cylce methods. One life cylce mehtod is componentwillmount.

- Link is a React component that ends up as an anchor tag. This can be used to link componentns or go frm one component to another

- in redux form we define form in component and this is later added to the application. Redux form handles the state of the form. That is holding the data in form. We still have to build the form. We define redux form state, design the form and wire up the two together.

- redux form injects some helpers to this.props. We can use it to wire form to redux form
