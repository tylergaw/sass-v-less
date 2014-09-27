## A bit of compare and contrast between Sass and Less

I'm making a decision on using Sass or Less on a project. Sass
is my preferred option because I'm used to it, but wanted to take
a look at Less before picking the default.

The examples are key areas that I noticed are different.

After the first tests I’m with Sass 100%.

Things to consider:
- Sass is Ruby, Less is JS. 1 point Less
- Less can't do rgba(red, 0.5) Sass can. 1 point Sass
- Less can't do %placeholder {stuff} .class {@extend %placeholder} Sass can. 1 point Sass
- Less's extend does not handle nested selectors by default (you have to include "all"). Sass does. 1 point Sass
- Less has the guarded mixin thing, Sass has funcs and conditionals. 1 point Sass
- To watch Less you have to install another thing. Sass has --watch built in. 1 point Sass

Score: Sass 5, Less 1

Things I was interested in testing:

After doing more research, **Sass/SCSS is the way to go**. The Ruby dependency is the only tiny downside and that seems like it's not going to be a bother at all.

There are some key reasons why Sass is the choice:

### Compiling/Watching

#### Sass
When you install Sass `(sudo) gem install sass` you get a watcher along with it. That means that you can watch `.scss` files or a directory and compile when the change with `sass --watch style.scss:style.css`

#### Less
When you install Less `npm install -g less` you you do not get any way to watch a file or directory. You have to use another tool to watch `.less` files and directories. [less-watch](https://www.npmjs.org/package/less-watch), Grunt, Gulp, Rake(yikes), etc.

Even though we'll most likely always use some type of build process that handles our CSS compilation, being able to just start watching is a big plus.

#### Placeholder selectors and Extend
Sass has the concept of placeholder selectors that you can use to store reusable CSS rules. You can either `@include` or `@extend` those. When you do, the placeholder selector is discarded. This is a good thing.

SCSS:
```scss
%base-styles {
  color: white;
  background-color: black;
  border: 1px solid red;
}

.box {
  @include %base-styles;
  font-size: 1.2em;
}
```

Output:
```css
.box {
  color: white;
  background-color: black;
  border: 1px solid red;
  font-size: 1.2em;
}
```

Less does not have the placeholder selector concept. You have to use a normal class and either include or extend it. The base class is included in the selector list even if it is never used.

Less:
```less
.base-styles {
  color: white;
  background-color: black;
  border: 1px solid red;
}

.box {
  .base-styles;
  font-size: 1.2em;
}
```

Output:
```css
.base-styles,
.box {
  color: white;
  background-color: black;
  border: 1px solid red;
  font-size: 1.2em;
}
```

#### Extend
Writing modular, reuseable CSS is very important for writing maintainable and efficient stylesheets. Both Sass and Less have the concept of extending a class. When you extend a class, the base styles are not included in the selector, the selector is added to the selector list of the base style.

Sass automatically included nested selectors. In the example, the `:hover` is the nested selector.

SCSS:
```scss
%common-button {
  background-color: blue;
  color: white;
  display: inline-block;
  text-decoration: none;

  &:hover {
    background-color: black;
  }
}

.small-button {
  @extend %common-button;
  font-size: 0.8em;
}

.med-red-button {
  @extend %common-button;
  background-color: red;
  font-size: 1.1em;
}

.big-button {
  @extend %common-button;
  font-size: 1.6em;
}
```

Output:
```css
.small-button, .med-red-button, .big-button {
  background-color: blue;
  color: white;
  display: inline-block;
  text-decoration: none;
}
.small-button:hover, .med-red-button:hover, .big-button:hover {
  background-color: black;
}

.small-button {
  font-size: 0.8em;
}

.med-red-button {
  background-color: red;
  font-size: 1.1em;
}

.big-button {
  font-size: 1.6em;
}
```

Less will included nested selectors, but you have to add an extra parameter. Wicked annoying. Also, not a fan of the syntax

Less:
```less
.common-button {
  background-color: blue;
  color: white;
  display: inline-block;
  text-decoration: none;

  &:hover {
    background-color: black;
  }
}

.small-button {
  &:extend(.common-button all);
  font-size: 0.8em;
}

.med-red-button {
  &:extend(.common-button);
  background-color: red;
  font-size: 1.1em;
}

.big-button {
  &:extend(.common-button);
  font-size: 1.6em;
}
```

Output:
```css
.common-button,
.small-button,
.med-red-button,
.big-button {
  background-color: blue;
  color: white;
  display: inline-block;
  text-decoration: none;
}
.common-button:hover,
.small-button:hover {
  background-color: black;
}
.small-button {
  font-size: 0.8em;
}
.med-red-button {
  background-color: red;
  font-size: 1.1em;
}
.big-button {
  font-size: 1.6em;
}
```

In all of these examples Sass is preferable (in my opinion)

## Reference:
- http://css-tricks.com/sass-vs-less/
- http://codepen.io/chriscoyier/blog/codepens-css
- http://markdotto.com/2014/07/23/githubs-css/
- http://mikeaparicio.com/2014/08/10/css-at-groupon/
- https://gist.github.com/fat/b27700946c777adacdf4
- https://medium.com/@fat/mediums-css-is-actually-pretty-fucking-good-b8e2a6c78b06
