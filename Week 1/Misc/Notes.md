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

* React is designed around the concept of reusable components. You define small components and you put them together to form bigger components. All components, big or small, are reusable, even accross different projects. A React component - in its simplest form - is a plain-old JavaScript function

* React Component names should start with a capital letter, every component recieves a list of attributes called props, and they use JSX (similar to HTML, but not HTML)

* Inside JSX, you can use any JavaScript expression within a pair of curly braces. JSX only allows expresssions (ternary okay, but not if statements)

* You can write React components with JavaScript classes (class Button extends React.Component)

* All React element attributes (events included) are names using camelCase, rather than lowercase. (onClick rather than onclick)

* We pass an actual JavaScript function reference as the event handler, rather than a string. (onClick={handleClick} not onClick="handleClick)