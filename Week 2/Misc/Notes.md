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

W2D3

* You want to freeze the arrays because you never want to mutate the state directly. Can use deepFreeze method of expect library

* Using concat, slice, or the spread operator will not modify the original array

* You also never want to modify the redux state directly. Object.freeze the oldState

* Use Object.assign to copy the object with the new assignments

* Mutations are not allowed in Redux 

* Object.assign lets you assign properties of several objects onto the target object. ie (Object.assign({}, oldState, {completed: !todo.completed}));

* The left argument is the one whose properties are going to be assigned, so it's going to be mutated. This is why we're passing an empty object as the first argument, so we don't mutate any existing data. Every further argument to Object.assign will be considered one of the source objects whose properties will be copied on to the target object

* It is important that if several sources specify different values for the same property, the last one wins. This is what we use to override the completed field despite what the original object says

* Object.assign is a new method in ES6, so it is not natively available in all the browsers. You should use a polyfill, either the one that ships withBabel or a standalone Object.assign polyfill, to use it without risking crashing your website

* Another option that doesn't require a polyfill is to use the new object spread operator, which is not part of ES6. However, it is proposed for ES7

```JS
const toggleTodo = (todo) => {
    return {
        ...todo,
        completed: !todo.completed
    };
}
```

* A reducer is a pure function that you write to implement the update logic of your application -- that is, how the next state is calculated given the current state and the action being dispatched.

W2D4

* Any time a function does too many things, you want to extract other functions from it and call them so that every function only addresses a single concern

* Reducer Composition - Different reducers specify how different parts of the state tree are updated in response to actions. Reducers are also normal JavaScript functions, so they can call other reducers to delegate and abstract a way of handling of updates of some parts of this tree they manage

* This pattern can be applied many times, and while there is still a single top level reducer managing the state of your app, you will fidnd it convenient to express it as many reducers that call on each other, each contribution to a part of the applications state tree

* Redux provides a function called combineReducers that lets you avoid writing this code by hand. Instead, it generates the top level reducer for you.

* The only argument to combineReducers is an objects. This object lets you specify the mapping between the state field names and the reducers managing them. 

* The return value of combineReducer is called a Reducer function, which is pretty much equivalent to the reducer function written previously by hand.

* Always name reducers after the state keys they manage. Since the key names and the value names are now the same, you can omit the values thanks to ES6 object literal shorthand notation

* The combineReducers function comes with Redux and generates one reducer from several other reducers, delegating to them paths of the same tree

W2D5

* Any state change is caused by a store.dispatch call somewhere in the component. When an action is dispatched, this store calls the reducer it was created with, with the current state and the action being dispatched.

* Presentational components are React components that don't specify any behaviors or have internal state, they are only concerned with how things look or how they render

* Presentational components will need container components to actually pass the data from the store and to specify the behavior

W2D6

* The components that access the store, such as the container level components, read this state from it, subscrivbe to this store, and dispatch actions on this store using a top-level store variable

* This works fine for examples, but it doesn't scale to real applications. First of all, it makes your container components harder to test because they reference a specific store, but you might want to supply a different mock store in the test. Secondly, it makes it very hard to implement universal replications that are rendered on the server, because on the server, you want to supply a different store instance for every request because different requests have different data.

* Every container component needs a reference to this store, so unfortunately we have to pass it down to every component as a prop. It's less effort than passing different data through every component, but it's still inconvenient. 

* The problem is that the container components need to have this store instance to get this state from a dispatch action and subscribe to changes. 