# babel-plugin-transform-scss

Babel plugin for converting scss or sass imports to css and embedding them in the head of the document

This plugin can be used for replacement of `sass-loader`

### How it works

This plugin will convert all scss or sass imports to the standard `<style>` attribute. For example:

```javascript
import React from 'react'
import 'style.scss'

const Button = () => {
  return (
    <div className="button">
      Custom button
    </div>
  )
}

export default Button
```

`import "style.scss"` will be transformed to css and will be added to the `head` of the `document`:

```html
<style data-scss-component="Button_style">
    .button {
      display: flex;
      justify-content: space-around;
    }
</style>
```

if import contains more than one styles:

```javascript
import React from 'react'
import 'style.scss'
import 'style2.scss'

const Button = () => {
  return (
    <div className="button">
      <div className="nested-from-style2">Nested</div>
    </div>
  )
}

export default Button
```
imported styles will be replaced like this:

```html
<style data-scss-component="Button_style">
    .button {
      display: flex;
      justify-content: space-around;
    }
</style>
<style data-scss-component="Button_style2">
    .nested-from-style2 {
      display: grid;
    }
</style>
```
