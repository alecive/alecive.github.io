# Testing

To test the website, I use [`html-proofer`](https://github.com/gjtorikian/html-proofer).

Example:

```
htmlproofer --only-4xx --checks-to-ignore ImageCheck,ScriptCheck ./_site/
```
