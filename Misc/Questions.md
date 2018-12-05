# Week 1

1. Name 5 benefits of HTML5

    1. Video and Audio tags
    2. Local storage
    3. Game development and interaction with Canvas
    4. Optimized for mobile development
    5. Legacy/cross browser support

2. What is localStorage? How might you use it?
- Local storage is HTML5's ability to store data on the client side browser, allowing you to retain the state of an application, cache data, or store user preferences

3. Why are media queries useful?
- You can tailor an application so it uses the space available to it, ie make things larger on mobile devices and smaller and spaced out on desktops

4. What is mobile-first design? Be as specific as possible.
- Designing for mobile devices before designing for desktop or other devices. This will make the page display faster on smaller devices. Instead of changing styles when the width gets smaller, we should change when the width gets larger

5. Give a high level overview of how CSS grids work.
- For CSS grid, you can define how many rows and columns you want and what the size of each should be. For example, you could have a grid-template-column of 100px 100px 100px and a grid-template-row of 200px 200px and this would create a grid with 3 columns of 100 px and two rows of 200px. Items placed into this grid will fill that space. Individual items can also be changed to take up different portions of the grid

6.  In which order do the React Lifecycle methods (including the optional ones) run?
- componentWillMount, componentDidMount, componentWillReceiveProps, shouldComponentUpdate, componentWillUpdate, componentDidUpdate, componentWillUnmount

7. In which lyfecycle methods should you make asynchronous fetches for data?
- componentDidMount or componentDidUpdate

8. In which lyfecycle methods can you call setState?
- componentDidMount, componentWillReceiveProps, componentDidUpdate

9. What are the React lifecycle methods? What are the use cases for each of those methods?
- 1. componentWillMount - component is about to mount, can be used for App configuration and setting up external APIs for root component
2. componentDidMount - component is on the page, used to start AJAX calls to load in data for the component
3. componentWillReceiveProps - component is about to get new props, takes in nextProps, can compare to current props and act on particular prop changes to trigger state transisitions
4. shouldComponentUpdate - component has received new props and wants to know if it should update. Defaults to true. Can be used to control exactly when component will re-render
5. componentWillUpdate - component has decided to update. Can be used instead of componentWillReceiveProps if the component also has shouldComponentUpdate, but no access to previous props
6. componentDidUpdate - component successfully updated. Can be used the same way as componentDidMount. Used to update the DOM in response to prop or state changes
7. componentWillUnmount - the component is about to disappear. Used to cancel any leftover requests or eventListeners on the component

10. Give one explanation for why we have to make AJAX requests in componentDidMount
- If you try to make the AJAX request before the component is mounted, you can't guarantee that the AJAX request won't resolve before the component mounts. If it did, you'd by trying to call setState on an unmounted component, which will raise an error. Calling AJAX in componentDidMount ensures that there is a component to update


# Week 2

1. What is a state tree in the context of Redux?
- A state tree in Redux is a single JavaScript object that contains all of the information and changes in the application, including the data and UI state

2. Why don't we want to modify (i.e. mutate) our redux state?
- It keeps code reliable and predictable. You don't have to specifically make anything in the state as long as the actions work and if the actions are the only thing that touches the state, you won't accidentally change it when you don't intend to

3. What is a pure function? Impure function?
- A pure function is one whose returned value depends solely on the values of their arguments. They do not have observable side effects, such as network or database calls, they are predictable, and they do not modify the values passed to them. An impure functions may call the database or the network, they may have side effects, may operate on the DOM, and may override the values given to them

4. Describe in detail what a redux reducer is. What makes it a pure function?
- The reducer takes in the previous state of the application and the action being dispatched and returns the next state of the app. It's a pure function because it does not modify the arguements given to it and has no side effects. It takes in the state and returns a new object based on the dispatched action.

5. What is the role of the store in Redux?
- The store binds together the 3 principles of Redux. It holds the current application's state object, it lets you dispatch actions, and when you create it, you need to specify the reducer that tells how the state is updated with actions. 

6. What does the subscribe method do in Redux?
- The subscribe method lets you register a callback that the redux store will call any time an action has been dispatched, so that you can update the UI of your application. It will reflect the current application state