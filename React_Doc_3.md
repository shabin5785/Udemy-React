- The first part of a JSX tag determines the type of the React element.
Capitalized types indicate that the JSX tag is referring to a React component. These tags get compiled into a direct reference to the named variable, so if you use the JSX <Foo /> expression, Foo must be in scope.

- Since JSX compiles into calls to React.createElement, the React library must also always be in scope from your JSX code. So even if we are not directly referring to React, as we are using JSX React must be in scope


