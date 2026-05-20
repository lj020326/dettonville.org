
Setup Notes
====

## Building
To build site html, run

```bash
hugo
```
## Testing
To test, run

```bash
hugo serve
## OR
hugo server --gc --minify --disableFastRender
```

## To Deploy
To deploy site, run

```bash
cd public

git add . && git commit -a -m 'updates'
git push origin
```
