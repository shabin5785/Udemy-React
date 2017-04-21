### Reconciliation

-React provides a declarative API so that you don't have to worry about exactly what changes on every update. This makes writing applications a lot easier, but it might not be obvious how this is implemented within React
When you use React, at a single point in time you can think of the render() function as creating a tree of React elements. On the next state or props update, that render() function will return a different tree of React elements. React then needs to figure out how to efficiently update the UI to match the most recent tree.

There are some generic solutions to this algorithmic problem of generating the minimum number of operations to transform one tree into another. However, the state of the art algorithms have a complexity in the order of O(n3) where n is the number of elements in the tree.

 Instead, React implements a heuristic O(n) algorithm based on two assumptions:

	Two elements of different types will produce different trees.
	The developer can hint at which child elements may be stable across different renders with a key prop.
In practice, these assumptions are valid for almost all practical use cases.

**The Diffing Algorithm**
-When diffing two trees, React first compares the two root elements. The behavior is different depending on the types of the root elements.
Whenever the root elements have different types, React will tear down the old tree and build the new tree from scratch. Going from <a> to <img>, or from <Article> to <Comment>, or from <Button> to <div> - any of those will lead to a full rebuild.
When tearing down a tree, old DOM nodes are destroyed. Component instances receive componentWillUnmount(). When building up a new tree, new DOM nodes are inserted into the DOM. Component instances receive componentWillMount() and then componentDidMount(). Any state associated with the old tree is lost.
Any components below the root will also get unmounted and have their state destroyed.

> <div
  <Counter /
</div
<span
  <Counter /
</span

This will destroy the old Counter and remount a new one.

-When comparing two React DOM elements of the same type, React looks at the attributes of both, keeps the same underlying DOM node, and only updates the changed attributes. 

> <div className="before" title="stuff" /
<div className="after" title="stuff" /

By comparing these two elements, React knows to only modify the className on the underlying DOM node.
When updating style, React also knows to update only the properties that changed. For example:

> <div style={{color: 'red', fontWeight: 'bold'}} /
<div style={{color: 'green', fontWeight: 'bold'}} /

When converting between these two elements, React knows to only modify the color style, not the fontWeight.
After handling the DOM node, React then recurses on the children.

-When a component updates, the instance stays the same, so that state is maintained across renders. React updates the props of the underlying component instance to match the new element, and calls componentWillReceiveProps() and componentWillUpdate() on the underlying instance.
Next, the render() method is called and the diff algorithm recurses on the previous result and the new result.

-By default, when recursing on the children of a DOM node, React just iterates over both lists of children at the same time and generates a mutation whenever there's a difference.

<a><b> <a><b><c>

The above is efficient. React can keep a and b and add c. But if we add c at beginnig, react has to tear down all teh elements leading to poor performance

**Keys**
In order to solve this issue, React supports a key attribute. When children have keys, React uses the key to match children in the original tree with children in the subsequent tree. So just add key to the list (answer to why we need keys in lists in React)

-It is important to remember that the reconciliation algorithm is an implementation detail. React could rerender the whole app on every action; the end result would be the same. We are regularly refining the heuristics in order to make common use cases faster.

1. The algorithm will not try to match subtrees of different component types. If you see yourself alternating between two component types with very similar output, you may want to make it the same type. In practice, we haven't found this to be an issue.
2. Keys should be stable, predictable, and unique. Unstable keys (like those produced by Math.random()) will cause many component instances and DOM nodes to be unnecessarily recreated, which can cause performance degradation and lost state in child components.








