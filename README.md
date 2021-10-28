# [gh-pages-securitytxt.github.io](https://gh-pages-securitytxt.github.io)
Example site showing how GitHub Pages supports `security.txt` files.

GitHub Pages (gh-pages) is static site hosting, so certain features like configuring
mime types for different file extensions or server 301/302 redirects aren't possible.

See [security.txt](https://github.com/securitytxt/security-txt) for more information
on what this file is for.

The following should work:
- <https://gh-pages-securitytxt.github.io/security.txt> (static)
- <https://gh-pages-securitytxt.github.io/.well-known/plain_security.txt> (static)
- <https://gh-pages-securitytxt.github.io/.well-known/security.txt> (redirects to
`/security.txt`)


### .well-known/ Note

For this directory to work in GitHub Pages, you need to set
`include: [".well-known"]` in the `_config.yml` file.

### Static 'txt' files

GitHub Pages recognises `.txt` files and sets the mime type correctly to `text/plain`.

### Redirect `txt` _files_

_Note: that you should only redirect to another `security.txt` file (useful if
centrally managed)._

It's best to use a 301/302 server redirect, however there's currently no way to
configure these with GitHub Pages.

You also can't configure content types with GitHub Pages. With some static hosting
(like AWS S3) you could create HTML files, save them with `.txt` file extension,
and set their content type to `text/html` - browsers will treat the files as HTML
and would action any redirects in the HTML.

However, for GitHub Pages, you need to create a `security.txt` _directory_ and
a `index.html` file with the redirecting HTML in.

Here's an example of `index.html` content to use (replacing `DOMAIN` for your own):

``` html
<!DOCTYPE html>
<html>
  <head>
    <link rel="canonical" href="https://DOMAIN/.well-known/security.txt" />
    <meta http-equiv=refresh content="0; url=https://DOMAIN/.well-known/security.txt" />
    <meta name="robots" content="noindex,follow" />
    <meta http-equiv="cache-control" content="no-cache" />
  </head>
  <body>
  </body>
</html>
```
...placed in directories, like:
- `blah.github.io/.well-known/security.txt/index.html`
- (optionally) `blah.github.io/security.txt/index.html`

---

## Middleman `config.rb` Configuration

### Static files
Add a `security.txt` file with the filename `security.txt.erb`, and `_config.yml`
(see `.well-known/ Note` above) to your source directory. 

```
- source
  - security.txt.erb
  - _config.yml
```

The following config imports the `_config.yml` file that would normally be ignored and
_proxies_ the `security.txt` template file in the `.well-known` directory.

``` ruby
import_file File.expand_path("_config.yml", config[:source]), "/_config.yml"
proxy("/.well-known/security.txt", "security.txt", ignore: false)
```

### Redirects
Add/configure `_config.yml` (see `.well-known/ Note` above) in your source directory. 

```
- source
  - _config.yml
```

The following config uses
[Middleman's redirect](https://middlemanapp.com/basics/redirects/) to create `index.html`
files in the `security.txt` and `.well-known/security.txt` _directories_ (replacing
`DOMAIN` for your own).

``` ruby
import_file File.expand_path("_config.yml", config[:source]), "/_config.yml"
redirect "security.txt/index.html", to: "https://DOMAIN/.well-known/security.txt"
redirect ".well-known/security.txt/index.html", to: "https://DOMAIN/.well-known/security.txt"
```
