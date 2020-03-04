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
