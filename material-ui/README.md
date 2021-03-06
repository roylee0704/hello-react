## material-ui

This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app) and [Material UI](https://material-ui.com/getting-started/installation/) and react-router-dom.

## 1. Dependencies

### material-ui core

```sh
$ npm install @material-ui/core
```

### material-ui style

Yes, it's a [separate package](https://material-ui.com/styles/basics/) for `Css-in-JS` solution. And why do I need it? 

- out-of-box-solution for styling material-ui component (even though you don't have too).
- you can [style (css) dynamically based on current app state (js)](https://material-ui.com/styles/basics/#adapting-based-on-props).

```sh
$ npm install @material-ui/styles
```

## 2. [Styles](https://material-ui.com/styles/basics/)

There are 3 ways of using style-api:
- hook(`makeStyles`+`useStyles`). If your React supports hooks, use this for greater flexibility.
- higher-order(`withStyles`). It encapsulates `make-use hook` within the higher-order function - It calls `makeStyles` on input::style and `useStyle` that returns output::classes. If your React doesn't support hook or want to avoid hook's boilerplate, use this.
- styled-component(`styled`). Simplest, no class-name needed - hence only support styles for single component.


## 3. [Theming](https://material-ui.com/customization/theming/)

A way to override default Material-ui styles: `palette`, `typography`, `spacing`, `breakpoints`, `density`, `z-index`, `globals`.

It takes only 3 steps.

First, override theme with `createMuiTheme`. You may create new variables or override one of the existing variables (in [default theme](https://material-ui.com/customization/default-theme/?expand-path=$.palette)) nested under one of these objects: `palette`, `typography`, `spacing`, `breakpoints`, `density`, `z-index`, `globals`.

```js
const theme2 = createMuiTheme({
  status: {
    dangerous: blue[500],
    lol: orange[400]
  }
});
```

Then, freely wrap any components that you wish to **apply** customized theme with a `<ThemeProvider/>` React component.

```js
    <ThemeProvider theme={theme}>
        <CustomCheckbox />
    </ThemeProvider>
```

Finally, 

If you're creating new variables - inject `theme` obj into one of your Styling apis: `makeStyles`, `styled`, `withStyles`

```js
const useStyles = makeStyles((theme) => ({
  root: {
    color: theme.status.dangerous,
    "&$checked": {
      color: theme.status.lol
    }
  },
  checked: {}
}));
```

Else (merely modifying the existing theming variables...), just specify the defined class-name to corresponding props for one of these objects:
- `palette` -  `prop::color`.
- `typography` - `prop::variant`.
- `spacing` - no prop.
- `breakpoints` - no prop.
- `density` - no prop.
- `z-index` - no prop.
- `globals` - no prop.

```js
export default function Palette() {
  return (
    <ThemeProvider theme={theme}>
      <Button color="primary">Primary</Button>
      <Button color="secondary">Secondary</Button>
    </ThemeProvider>
  );
}
```

### 3.1 Palette

For color pairs (primary vs secondary), check [here](https://www.designwizard.com/blog/design-trends/colour-combination).

These are the main classes found in palette object:
- primary
- secondary
- error
- warning 
- info
- success
- text, background, etc...

To apply, just specify the class-name to `color` prop in any Material-ui component.
```js
export default function Palette() {
  return (
    <ThemeProvider theme={theme}>
      <Button color="primary">Primary</Button>
      <Button color="secondary">Secondary</Button>
    </ThemeProvider>
  );
}
```

## References

- https://www.udemy.com/course/implement-high-fidelity-designs-with-material-ui-and-reactjs/learn/lecture/16040478#overview
