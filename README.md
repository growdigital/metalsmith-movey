# metalsmith-move

![nodei.co](https://nodei.co/npm/metalsmith-move.png?downloads=true&downloadRank=true&stars=true)

![npm](https://img.shields.io/npm/v/metalsmith-move.svg)

![github-issues](https://img.shields.io/github/issues/leviwheatcroft/metalsmith-move.svg)

![stars](https://img.shields.io/github/stars/leviwheatcroft/metalsmith-move.svg)

![forks](https://img.shields.io/github/forks/leviwheatcroft/metalsmith-move.svg)

[metalsmith](metalsmith.io) plugin to edit file paths


## install

`npm i --save metalsmith-move`

## usage

Suppose your `src` contains three files:

```
articles/one.html
articles/two.html
articles/three.html
pages/about/projects.html
```

`move` would generate results like this in your `build` directory:
```
metalsmith()
.use(move({
  'articles/one.html'   : ':filename',              // one.html
  'articles/two.html'   : 'blog/:YYYY/:filename',   // blog/2016/two.html
  'articles/three.html' : ':title:extname'          // article-title.html
  'pages'               : ':relative:filename'      // about/projects.html
})
```

## tokens

__ from path __

 - *:filename* full filename, including extension, omits path
 - *:basename* filename excluding extension
 - *:extname* file extension, preceded by `.`
 - *:dirname* path from src directory
 - *:relative* path from specified mask directory (see usage example)

__ from moment __

basically any format tokens
[from moment](http://momentjs.com/docs/#/displaying/) including only 'D' or 'M'
or 'Y'. You need to specify a token for each value, as in:
`:YYYY-:MMMM/:filename`

If a `date` field is set in a file's frontmatter, then that value will be used,
otherwise `ctime` (file created time) is used instead. Note that moment can
only parse dates formatted in limited ways. You can patch the date parser as
shown in the example below.

__ from meta __

`move` will check the file's meta for token matches, so `:title` will convert
the file's title to a slug. You can patch the slug generation fn as shown above.

## options

```
.use(move(
  {
    'blog': ':YYYY/:MMMM/:title'
  },
  {
    date: (meta) => '2016-10-26',
    slug: (str)  => str.replace(/\s/g, '_')
  }
))
```

## Author

Levi Wheatcroft <levi@wht.cr>

## Contributing

Contributions welcome; Please submit all pull requests against the master
branch.

## License

 - **MIT** : http://opensource.org/licenses/MIT

