# Vue KaTeX Auto-render

KaTeX enables fast math typesetting for the web. **Vue KaTeX Auto-render** is a plugin to help you use KaTeX together with [auto-render extension of KaTeX](https://katex.org/docs/autorender.html).

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

### Requirements

Vue 2.x

### Installation


#### With NPM

```bash
npm install --save vue-katex-auto-render
```

#### With Yarn

```bash
yarn add vue-katex
```

#### Make it work with Vue

You have to import it and register it as a custom directive.

```javascript
import Katex from 'vue-katex-auto-render'
Vue.directive('katex', Katex);
```

### Usage

You can use the `v-katex` directive on any element of your template. And then put the content that you expect KaTeX to deal within some `delimiters`. The `delimiters` is a list of delimiters to look for math. Each delimiter has three properties:

- left: A string which starts the math expression (i.e. the left delimiter).
- right: A string which ends the math expression (i.e. the right delimiter).
- display: A boolean of whether the math in the expression should be rendered in display mode or not.

The default value of delimiters for Vue KaTeX Auto-render is:

```javascript
[
  {left: "$$", right: "$$", display: true},
  {left: "$", right: "$", display: false},
  {left: "\\(", right: "\\)", display: false},
  {left: "\\[", right: "\\]", display: true}
]
```

Any content within given delimiters in the tags with `v-katex` marked will then be treated as something need to be processed by KaTeX.

For example,

```html
<template>
  <div v-katex>
    $$% Here is some comment
    f({x}) = \int_{-\infty}^\infty\hat f(\xi)\,e^{2 \pi i \xi x}
    \,d\xi$$
  </div>
</template>
```

The code above will have the following as an output.

![image](https://user-images.githubusercontent.com/2560088/66028880-9acfa080-e530-11e9-8d6b-620ac0afd14c.png)

#### More Configurations

You may also pass some configurations to customize the result. For example, if you only want to support rendering KaTeX within same mark like `[KaTeX_start]...[Katex_end]` you can do something like:

```html
<template>
  <div v-katex="options">
    [KaTeX_start]f({x}) = \int_{-\infty}^\infty\hat f(\xi)\,e^{2 \pi i \xi x}\,d\xi[KaTeX_end]
  </div>
</template>
<script>
export default {
  data: function() {
    return {
      options: {
        delimiters: [
          {left: "[KaTeX_start]", right: "[KaTeX_end]", display: true}
        ]
      }
    };
  }
}
</script>
```

Beside the option of `delimiters`, you can set `ignoredTags`, `ignoredClasses`, `errorCallback`, `preProcess`, etc as you need. You may refer to document of [Auto-render Extension](https://katex.org/docs/autorender.html) for further descriptions of the these options.

### License

Vue KaTeX Auto-render is released under the [MIT license](http://opensource.org/licenses/MIT).
