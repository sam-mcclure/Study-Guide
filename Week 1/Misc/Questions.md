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