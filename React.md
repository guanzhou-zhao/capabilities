## Refs

#### Use cases of Refs
- Managing focus, text selection, media playback
- Triggering imperative animation
- Integrating with third party framework

#### Avoid using refs for anyting that can be done declaratively
#### May not use ref attribute on function component, because they don't have instance.
#### API or usage
- `this.textInput = React.createRef() ... <input ref={this.textInput} />`
- Or `<input ref={element => this.textInput = element } />`

## Higher-Order Components
- Higer-Order Components are functions that takes a component and return a new component.
- HOC is not React API per se.
- HOC is a JavaScript pattern that embraces React's compositional nature.
- React Redux's `connect` is HOC.
- Use HOC for cross-cutting concerns.

#### Conventions of using HOC
- Don't mutate the original component. Use composition.
- Maximazing composition. HOC like `component => component` is easy to compose.
- Use displayName for easy debugging.
- Pass unrelated props to the wrapped component.

#### Caveats
- Don't use HOC in reder method.
- Ref can't be passed correctly.
- Static method must be copied over. `import hoistNonReactStatic from 'hoist-non-react-statics';`

## Forwarding Refs
```
class WrappedComponent extends React.Component {
  render() {
    const {forwardedRef, ...rest} = this.props;
    ...
  }
}
export default React.forwardRef((props, ref) => {
    return <WrappedComponent {...props} forwardedRef={ref} />;
  });
```

## Render Props
```
<DataProvider render={data => (
  <h1>Hello {data.target}</h1>
)}/>
```
- Render Props of a component is a prop named render which is a function that accepts data from the component and giving back customized dom or component
- Libraries that use render props include React Router, Downshift and Formik.
- One interesting thing to note about render props is that you can implement most higher-order components (HOC) using a regular component with a render prop.
```
// If you really want a HOC for some reason, you can easily
// create one using a regular component with a render prop!
function withMouse(Component) {
  return class extends React.Component {
    render() {
      return (
        // Mouse component passes mouse to Component, and decide where to render Component.
        <Mouse render={mouse => (
          <Component {...this.props} mouse={mouse} />
        )}/>
      );
    }
  }
}
```

## Uncontrolled Components
Use `ref` to get values from uncontrolled components.

## Reconciliation

#### Assumption:
- Two elements of different types produce different trees.
- Developers can hint at which elements stay stable between renders with `key` prop.

## Context

#### React.createContext Context.displayName
```
const LoggedInUserContext = React.createContext({name: "guest", tag: 0});
LoggedInUserContext.displayName = "LoggedInUserContext"
```
#### Context.Provider
```
<ThemeContext.Provider value="light">
  <LoggedInUserContext.Provider value={{name:"Ben", tag: 1}}>
    <h2>App component</h2>
    <Toolbar />
  </LoggedInUserContext.Provider>
</ThemeContext.Provider>
```
#### Context.Consumer
```
<LoggedInUserContext.Consumer>
  {
    (loggedInUser) => <h3>....Toolbar component Hi, {loggedInUser.name}</h3>
  }
</LoggedInUserContext.Consumer>
```
#### Class.contextType = Context   {this.context}

## Error Boundaries
- Use `<ErrorBoundary>` component to wrap subtree.
- Use `static getDerivedStateFromError()` to render a fallback UI
- Use `componentDidCatch()` to log error information.
- Where to put `<ErrorBoundary>` is up to you.
- Uncaught errors will result in unmounting of the whole React component tree.
- `<ErrorBoundary>` is only for imperative code.
- Use `try / catch` to catch the errors inside event handler.

## JSX
- JSX provide syntactic sugar for the `React.createElement(component, props, ...children)`.

## Optimizing Performance
- Use production build
- Profiling Components with the Chrome Performance Tab
- Virtualize long lists
- Avoid Reconciliation
- shouldComponentUpdate
- Not mutate data, use new one
