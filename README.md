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

## .well-known/

For this directory to work, you need to set `include: [".well-known"]` in the
`_config.yml` file.

## Static file

GitHub Pages recognised `.txt` files and sets the mime type correctly to
`text/plain; charset=utf-8`.

## How to do a redirect?

_Note: that you should only redirect to another `security.txt` file (useful if
centrally managed)._

You need to create a `security.txt` _directory_ and an `index.html` file with the
following content (replacing `DOMAIN` for your own):

``` html
<!DOCTYPE html>
<html>
  <head>
    <meta http-equiv="refresh" content="0; https://DOMAIN/.well-known/security.txt" />
  </head>
  <body>
    <p><a href="https://DOMAIN/.well-known/security.txt">https://DOMAIN/.well-known/security.txt</a></p>
  </body>
</html>
```
...so `blah.github.io/.well-known/security.txt/index.html` and optionally
`blah.github.io/security.txt/index.html`.
