- Layout Components: They help arrange components in a section of the page (i.e. Modals, Split Screen)
> NOTE: Components shouldn't care were they are located

- Container Components: They load the required data and pass it as props to the children, they usually have the word "loader" in them (i.e. UserLoader)

- Uncontrolled Components: Components that manage their own state. The application only knows about it when an event happens
- Controlled Components: Components that rely on their parent to handle their state
> NOTE: We usually prefer controlled components since they're more reusable and easier to test

- High-Order Components (HOCs): They are used to add functionality to an existing component. They are a component that return another component

- Custom Hooks: Encapsulate multiple hooks and logic within a single hook (It's basically a function that runs multiple hooks)

- Recursive Components: Components that use themselves (they could be used for things like a treeview)

- Component Composition: Have a component that uses another lower-level component with some props already set (i.e. Button component, and then a DangerButton component that sets the color of that Button component to red, and any other stuff)

- Partially Applied Components: Use a HOC to create the component composition


