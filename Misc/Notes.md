# Week 1

* 10 Reasons to use HTML5: 

1. It's the future - Everyone's going to be using it

2. Mobile - HTML5 is most mobile ready tool for developing mobile sites and apps

3. Legacy/Cross Browser Support - Modern popular browsers and old ones like IE6 all recognize the HTML doctype, though not all features are supported

4. Game Development - Can develop games using canvas

5. Better Interactions - Canvas HTML tag allows you to have iteractive and animated content without outside plugins. Among several other APIs

6. Smarter Storage - Has a local storage feature. A cross between cookies and a client-side database. It's better than cookies because it allows for storage across multiple windows, it has better security and performance,and data will persist even after the browser is closed. You don't have to worry about a user deleting cookies.
Being able to store data in the user's browser allows you to easily recreate those app features like: storing user information, the ability to cache data, and the ability to load a user's previous application state.

7. Cleaner Code - Allows you to write clear and descriptive code, semantic code that allows you to easily separate meaning from style and content

8. Doctype - <!DOCTYPE html> single, simple doctype

9. Video and Audio Support - HTML5 has <video> and <audio> tags, getting rid of the need for Flash Player and other third party media players

10. Accessibility - HTML5 makes creating accessible sites easier for two main reasons: semantics and ARIA. The new HTML headings like <header>, <footer>, and <nav> allow screen readers to easily access content. ARIA is a W3C spec that is mainly used to assign specific rols ro elements in an HTML document, essentially creating important landmarks on the page.

# CSS

## Media Query

- Media query is a CSS3 technique. It uses the @media rule to include a block of CSS properties only if a certain condition is true. You can add a size breakpoint where certain parts of the design will behave differently on each side of the breakpoint

- Always design for mobile first. Should change design when width gets larger instead of smaller

- Media queries can also be used to change layout of a page depending on the orientation of the browser. You can also hide elements on different screen sizes

## CSS Grid

* Grid layouts are fundamental to the design of websites and the CSS grid module is the most powerful and easiest tool for creating it

* The two core ingredients of a CSS Grid are the wrapper(parent) and the items(children). The wrapper is the actual grid and the items are the content inside the grid

* To turn the wrapper div into a grid, you simply give it a display property of grid

* To make the grid two-dimensional, we'll need to define the columns and rows. You can use the grid-template-row and grid-template-column properties. You get as many rows/columns as you fill in values for( ie grid-template-columns: 100px 100px 100px; makes 3 columns)

* In order to resize specific items in a grid, you can use grid-column-start and grid-column-end to make a specific item take up multiple column spaces. Or grid-column 1/4

W1D4

## React

* Through lifecycle methods, we can control what happens when each tiny section of the UI renders, updates, thinks about re-rendering, and then disappears entirely

* **componentWillMount** - Your component is about to appear on the screen and render is about to be called. There is no component yet, so you can't do anything involving the DOM. Nothing has changed since your component's constructor was called, which is where you should be setting up your component's default config. Not much use. 
- The component is in default position. Almost everything should be taken care of by the rest of your component code, without the complication of an additional lifecycle method
- The exception is any setup that can only be done at runtime - namely connecting to external APIs. Such configuration should be done at the highest level component (root), so 99% of components should not use componentWillMount
- Some people might use this to start AJAX calls to load data for components. Don't do this.
- Most common use case: App configuration in your root component
- don't call setState, use default state instead

* **componentDidMount** - The component is mounted and ready to be used. Here is where you load in data. You can't guarantee the AJAX request won't resolve before the component mounts. If it did, that would mean that you'd be trying to setState on an unmounted component, which won't work and will give an error. Doing AJAX in componentDidMount will guarantee that there's a component to update.
- Where you can do all the fun things you couldn't do when there was no component, such as: draw on a canvas element, initialize a grid layout, add event listeners, etc
- Basically, here you want to do all the setup you couldn't do without a DOM, and start getting all the data you need.
- Most common use: Starting AJAX calls to load in data for your component
- Can call setState

* **componentWillReceiveProps** - The component is working and it is about to recieve some new props. Perhaps some data that was loaded in by a parent's componentDidMount finally arrived, and is being passed down. Before the component does anything with the new props, this method is called with nextProps as the argument
- componentWillReceiveProps(nextProps)
- Has access to both the nextProps and current props. Check which props will change(can sometimes be called when nothing has changed) and if the props will change in a significant way, act on it
- Not called on initial render
- Most common use: Acting on particular prop changes to trigger state transitions
- Can call setState

* **shouldComponentUpdate** - Component has recieved new props. Typically when a component receives new props or new state, it should update, but it's going to ask for permission first
- shouldComponentUpdate(nextProps, nextState)
- Should always return a boolean (the answer to 'should I rerender?"). Always returns true by default
- Can be used to improve performance
- Only update if the props you care about change. React component will not update normally, so use with caution
- Most common use: Controlling exactly when your component will re-render
- Can not call setState

* **componentWillUpdate** - The component has committed to updating and asks if it should do anything before re-render. Basically the same as componentWillRecieveProps, not very useful
- If you're using shouldComponentUpdate AND need to do something when props change, using componentWillUpdate would make sense, but it's probably not going to give a lot of additional utility
- Most common use: Used instead of componentWillReceiveProps on a component that also has shouldComponentUpdate (but no access to previous props)
- Can not call setState

* **componentDidUpdate** - The component successfully updated. Here we can do the same stuff we did in componentDidMount(get data, redraw canvas, etc). In componentDidUpdate, you don't know why it updated
- Most common usage: Updating the DOM in response to prop or state changes
- Can call setState

* **componentWillUnmount** - The component is about to disappear, but it can make a last-minute request. Here, you can cancel any outgoing network requests or remove all eventListeners associated with the component
- Basically, clean up anything to do that solely involves the component in question, when it's gone, it should be completely gone
- Most common use: Cleaning up any leftover debris from your component
- Can not call setState

# Week 2

## Redux

* The first principle of Redux is that no matter the app, you are going to represent the whole state of the app as a single JavaScript object

* All mutations and changes in the Redux state are explicit. It is possible to keep track of all of them. 

* The first principle of Redux: everything that changes in your application, including the data and the UI state, is contained in a single object, that we call the state or the state tree

* The second principle of Redux is that the state tree is read only. You cannot modify or write to it. Instead, any time you want to change the state, you need to dispatch an action.

* An action is a plain JavaScript object describing the change. Just like the state is the minimal representation of the data in your app, the action is the minimal representation of the change to that data.

* The structure of the action object is up to you. The only requirement is that it has a type property, which is not undefined. You should use strings because they are serializable

* The second principle of Redux: the state is read-only. The only way to change the state tree is by dispatching an action. An action is a plain JavaScript object, describing the minimal way what changed in the application. Whether it was initiated by a network request or by a user interaction, any data that gets into the Redux application gets there by actions.

* Pure functions are those whose returned value depends solely on the values of their arguments. They do not have any observable side effects, such as network or database calls. The pure functions just calculate the new value. You can be confident that if you call the pure function with the same set of arguments, you're going to get the same returned value. They are predictable. They also do not modify the values passed to them

* Impure functions may call the database or the network, they may have side effects, they may operate on the DOM, and they may override the values that you pass to them.

* The UI or the view layer is most predictable when it is described as a pure function of the application state. Redux complements this approach with another idea, that the state mutations in your app need to be described as a pure function that takes the previous state and the action being dispatched and returns the next state of your application 

* Inside any Redux application, there is one particular function that takes the state of the whole application and the action being dispatched and returns the next state of the whole application. It is important that it does not modify the state given to it. It has to be pure, so it has to return a new object.

* The third and last principle of Redux: to describe state mutations, you have to write a function that takes the previous state of the app, the action being dispatched, and returns the next state of the app. This function has to be pure. This is called the Reducer.

11.28.18

* Reducer accepts state and action as arguments and returns the next state

* Can test reducer with expect library

* If the reducer receives undefined as the state argument, it must return what it considers to be the initial state of the application. If it receieves an unknown action, it should return the current state

* example reducer: 
```js
const counter = (state = 0, action) => {
    switch (action.type){
        case 'INCREMENT':
            return state + 1;
        case 'DECREMENT':
            return state - 1;
        default:
            return state;
    }
}
```

* Import create store from redux npm package. This store binds together the 3 principles of Redux. It holds the current application's state object, it lets you dispatch actions, and when you create it, you need to specify the reducer that tells how the state is updated with actions.

* The store has 3 important methods:
    1. getState - It retrieves the current state of the Redux store
    2. dispatch - It lets you dispatch actions to change the state of your application.
    3. subscribe - Lets you register a callback that the Redux store will call any time an action has been dispatched, so that you can update the UI of your application It will reflect the current application state

* You can subscribe the render method to the store

* We know that the store holds the current state. We keep it in a variable and the getState function is going to return the current value of that variable. This function, combined with the dispatch function and a subscribe function on a single object is what we call the Redux store

* Because the subscribe function can be called many times, we need to keep track of all the changed listeners. Any time it is called, we want to push the new listener into the array. Dispatching an action is the only way to change the internal state.

* In order to calculate the new state, we call the reducer with the current state and the action being dispatched. After the state was updated, we need to notify every changed listener by calling it. Instead of adding a dedicated unsubscribe method, we'll just return a function from the subscribe method that removes this listener from the listeners array

* By the time the store is returned we wanted to have the initial state populated. We're going to dispatch a dummy action just to get the reducer to return the initial value. 

* Implementation of Redux store:
```JS
const createStore = (reducer) => {
    let state;
    let listeners = [];

    const getState = () => state;

    const dispatch = (action) => {
        state = reducer(state, action);
        listeners.forEach(listener => listener());
    };

    const subscribe = (listener) => {
        listeners.push(listener);
        return () => {
            listeners = listeners.filter(l => l !== listener);
        };
    };

    dispatch({});

    return { getState, dispatch, subscribe };
}

const store = createStore(reducer);

```

* By adding React and React-dom packages and a root div to render to, you can call ReactDOM.render within the root component. The render function is called any time this store state changes, so you can safely pass the curent state of this store as a prop to the root component.

* The counter component is a dumb component. It does not contain any business logic, it only specifies how the current application state transforms into renderable output and how the callbacks, passed via props, are bound to the event handlers.

* Finally, we subscribe to the Redux Store, so out render function runs anytime the state changes, so the counter gets the current state

