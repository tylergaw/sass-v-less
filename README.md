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

## Reference:
- http://css-tricks.com/sass-vs-less/
- http://codepen.io/chriscoyier/blog/codepens-css
- http://markdotto.com/2014/07/23/githubs-css/
- http://mikeaparicio.com/2014/08/10/css-at-groupon/
- https://gist.github.com/fat/b27700946c777adacdf4
- https://medium.com/@fat/mediums-css-is-actually-pretty-fucking-good-b8e2a6c78b06
