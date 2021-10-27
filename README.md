# [gh-pages-securitytxt.github.io](https://gh-pages-securitytxt.github.io)
Example site showing how GitHub Pages supports `security.txt` files.

GitHub Pages (gh-pages) is static site hosting, so certain features like configuring
mime types for different file extensions or server 301/302 redirects aren't possible.

See [security.txt](https://github.com/securitytxt/security-txt) for more information
on what this file is for.

Ideally, the following should work<sup>1</sup>:
- <https://gh-pages-securitytxt.github.io/plain_security.txt>
- <https://gh-pages-securitytxt.github.io/redirect_security.txt>
(redirect to another URL<sup>2</sup>)
- <https://gh-pages-securitytxt.github.io/.well-known/plain_security.txt>
- <https://gh-pages-securitytxt.github.io/.well-known/redirect_security.txt>
(redirect to another URL<sup>2</sup>)

The following _static_ files are also set up for the expected paths:
- <https://gh-pages-securitytxt.github.io/security.txt>
- <https://gh-pages-securitytxt.github.io/.well-known/security.txt>

<sup>1</sup> : using `plain_`/`redirect_` to try direct or redirecting `security.txt` 
files respectively, normally just `/security.txt` or `/.well-known/security.txt`
would be used

<sup>2</sup> : should redirect to https://gotsecuritytxt.com/.well-known/security.txt
in these test cases
