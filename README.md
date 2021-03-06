# metalsmith-movey

Total clone fork of [metalsmith-move](https://github.com/leviwheatcroft/metalsmith-move) by [Levi Wheatcroft](https://github.com/leviwheatcroft/), because [Netlify](https://www.netlify.com/) can't deploy metalsmith plugin from [GitHub](https://github.com/), it has to be on [npmjs.com](https://www.npmjs.com/)

Please don't rely on this clone fork, please bug Levi to publish his plugin ;)

[metalsmith](metalsmith.io) plugin to edit file paths


## install

`npm i --save metalsmith-movey`

## usage

The plugin accepts a single argument in the form `{src: format, ...}` like so:

```javascript
metalsmith.use(move({
  'articles': '{-title}{ext}',
  'pages': '{relative}/{base}'
}))
```

this call would move paths like this:

```
articles/one.html           >   article-one-title.html
articles/two.html           >   article-two-title.html
pages/about/projects.html   >   about/projects.html
```

`src` can be any multimatch mask. `format` can be any
[metalsmith-interpolate](https://github.com/leviwheatcroft/metalsmith-interpolate) format string.

## tokens

__ standard tokens __
Anything from [metalsmith-interpolate](https://github.com/leviwheatcroft/metalsmith-interpolate) is available, check that package for
details but for quick reference:

 * path tokens like: root, dir, name, base, ext
 * meta tokens like: title, author, or anything else in your front matter
 * date tokens like: {YY/MM/DD} (any moment format)
 * put a `-` or `_` infront of the token to slugify like `{-title}`

__ relative path __
This package provides a `{relative}` token, as shown in the example above this
token provides the relative path from the specified src directory. This token
is only available where `src` specifies a directory as shown in the examples
above.

## options

There's not really any options :-/

## Author

Levi Wheatcroft <levi@wht.cr>

## Contributing

Contributions welcome; Please submit all pull requests against the master
branch.

## License

 - **MIT** : http://opensource.org/licenses/MIT
