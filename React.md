## Refs

### Use cases of Refs
- Managing focus, text selection, media playback
- Triggering imperative animation
- Integrating with third party framework

### Avoid using refs for anyting that can be done declaratively
### May not use ref attribute on function component, because they don't have instance.
### API or usage
- `this.textInput = React.createRef() ... <input ref={this.textInput} />`
- Or `<input ref={element => this.textInput = element } />`

## Higher-Order Components
- Higer-Order Components are functions that takes a component and return a new component.
- HOC is not React API per se.
- HOC is a JavaScript pattern that embraces React's compositional nature.
- React Redux's `connect` is HOC.
- Use HOC for cross-cutting concerns.

### Conventions of using HOC
- Don't mutate the original component. Use composition.
- Maximazing composition. HOC like `component => component` is easy to compose.
- Use displayName for easy debugging.
- Pass unrelated props to the wrapped component.

### Caveats
- Don't use HOC in reder method.
- Ref can't be passed correctly.
- Static method must be copied over. `import hoistNonReactStatic from 'hoist-non-react-statics';`
