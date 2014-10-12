Disqus integration for GitBook
==============

You can use install it via **NPM**:

```
$ npm install gitbook-plugin-disqus
```

And use it for your book with:

```
$ gitbook build ./ --plugins=disqus
```


You can set the Disqus shortname using the plugins configuration in the book.json:

```
{
    plugins: ["disqus"],
    pluginsConfig: {
        "disqus": {
            "shortName": "XXXXXXX"
        }
    }  
}
```

