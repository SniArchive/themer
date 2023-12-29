# Themer

- Guide to easily add themes in your website using 'theme-change'
- This is not a library. This is a guide for the 'theme-change' library with snippets

# Demo

- Default device theme demo on [snipc's website](https://github.com/realsnipc/website)

# Setup

- Install 'theme-change' in your project. Refer to the [orignal repository](https://github.com/saadeghi/theme-change)

## CSS

Set your themeable style as custom properties in CSS like this:

```css
:root {
  --my-color: #fff;
  /* or any other variables/style */
}
[data-theme='dark'] {
  --my-color: #000;
}
[data-theme='pink'] {
  --my-color: #ffabc8;
}
```

then use your variables on any element

```css
body {
  background-color: var(--my-color);
}
```

## Options


- ### Default 

```
localStorage.setItem('theme', 'your default theme here');
```

- ### Set to device's default theme

```
    if (localStorage.getItem("theme") === null) {
      if (window.matchMedia && window.matchMedia('(prefers-color-scheme: dark)').matches) {
        localStorage.setItem('theme', 'dark');
      } else if (window.matchMedia && window.matchMedia('(prefers-color-scheme: light)').matches) {
        localStorage.setItem('theme', 'light');
      }
```


## HTML

There are 3 options:

- ### Using buttons to set a theme

  [![btn](https://user-images.githubusercontent.com/7342023/101527827-c0adcc00-39a3-11eb-9e41-24bfa91ea96c.gif)](#)

  Clicking on these buttons, sets the chosen theme and also adds the `ACTIVECLASS` to the chosen button

  ```
  <button data-set-theme="" data-act-class="ACTIVECLASS"></button>
  <button data-set-theme="dark" data-act-class="ACTIVECLASS"></button>
  <button data-set-theme="pink" data-act-class="ACTIVECLASS"></button>
  ```

- ### Toggle between two themes




  ```
  
    var item = localStorage.getItem('theme');
    if (item == "light") {
      document.querySelector('.theme').setAttribute("data-set-theme", "dark");
    } else if (item == "dark") {
      document.querySelector('.theme').setAttribute("data-set-theme", "light");
    }
  ```

- ### `<select>` menu

  [![select](https://user-images.githubusercontent.com/7342023/101527790-b4297380-39a3-11eb-9173-bc909549d160.gif)](#)

  ```
  <select data-choose-theme>
    <option value="">Default</option>
    <option value="dark">Dark</option>
    <option value="pink">Pink</option>
  </select>
  ```

# Advance use

<details>
<summary>
  Set theme based on OS color-scheme
</summary>

```css
@media (prefers-color-scheme: dark){
  :root{
    --my-color: #252b30;
  }
}
```

</details>

<details>
<summary>
  Use with PurgeCSS
</summary>

If you're using [Purge CSS](https://purgecss.com/), you might need to [safe list](https://purgecss.com/safelisting.html#in-the-css-directly) your CSS using the comments below because your secondary themes will be purged

- Safelist `[data-theme]` on postcss config

  ```js
  module.exports = {
    purge: {
      options: {
        safelist: [/data-theme$/],
      },
    },
  }
  ```

- Safelist inside CSS file

  ```css
  /*! purgecss start ignore */

  [data-theme='dark'] {
    --my-color: #252b30;
  }

  /*! purgecss end ignore */
  ```

</details>

<details>
<summary>
  Using custom localStorage key
</summary>

If you want to use a custom localStorage key, you can add it to the `data-key` attribute like this:

```html
<select data-choose-theme data-key="admin-panel">

<button data-key="front-page" data-set-theme="">

<span data-key="premium-user-theme" data-toggle-theme="dark">
```

</details>

---

[install-size]: https://badgen.net/bundlephobia/minzip/theme-change?label=bundle%20size&color=purple
[js]: https://badgen.net/badgesize/normal/https/unpkg.com/theme-change/index.js?label=file%20size&color=purple
[npm]: https://badgen.net/npm/v/theme-change?label=version&color=purple
[dl]: https://badgen.net/npm/dt/theme-change?icon=npm&color=purple
[commit]: https://badgen.net/github/last-commit/saadeghi/theme-change?icon=github&color=purple
[build]: https://badgen.net/github/checks/saadeghi/theme-change?label=build
[build-url]: https://github.com/saadeghi/theme-change/actions
[install-size-url]: https://bundlephobia.com/result?p=theme-change
[js-url]: https://unpkg.com/theme-change@latest/index.js
[npm-url]: https://www.npmjs.com/package/theme-change
[gh-url]: https://github.com/saadeghi/theme-change
