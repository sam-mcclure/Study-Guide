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