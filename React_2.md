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