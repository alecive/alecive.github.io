# Testing

To test the website, I use [`html-proofer`](https://github.com/gjtorikian/html-proofer). Adding automatic testing via `travis` would be nice, but for such a simple website it seems an overkill.

Example:

```
htmlproofer --only-4xx --checks-to-ignore ImageCheck,ScriptCheck ./_site/
```
