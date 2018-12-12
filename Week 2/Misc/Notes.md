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

