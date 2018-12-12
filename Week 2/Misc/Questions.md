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