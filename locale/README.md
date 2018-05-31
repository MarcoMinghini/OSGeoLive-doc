
# Locale

**Warning** for administrators only

**Note** Different versions of sphinx-intl change the `pot` and `po` files structure even with the same content

For generating the pot files v0.9.10 of sphinx-intl is used

- Installing the tx client: https://docs.transifex.com/client/installing-the-client
- Introduction to the client: https://docs.transifex.com/client/introduction
- Sphinx-intl installation: https://pypi.python.org/pypi/sphinx-intl
  ```
  pip install sphinx-intl==0.9.10
  pip show sphinx-intl
  ```
- Sphinx: http://www.sphinx-doc.org/en/stable/intl.html


Follow the steps in the order presented in this README

## build the pot/po files

```
cd build
rm -rf *
cmake  -DLOCALE=ON ..
make locale > locale_log.txt
cd ..
```

## Verifying changes

### List .pot files that changed
```
git diff --name-only | grep '\.pot'
```


### Verify the changes on the config file for transifex
```
git diff .tx/config
```

## Push changed resources to transifex

```
bash scripts/push_transifex.sh
```

## Commit changes

```
git commit -a -m 'Updating the locale'
```

## Pull transtlated strings

One file regardles of translation completition, normally used while translating.

**Note:** Don't commit incomplete translations
```
tx pull -r osgeolive.overview--52nSOS_overview -l fr 
```

All the 100% translated files of French language.
* Takes time
* This you can commit and make a PR
```
tx pull -l fr --minimum-perc=100 --skip
```

## clean the build & build the documentation:

Use capital letters for the language, this builds for French
```
cd build
rm -rf *
cmake  -DHTML=ON -DFR=ON..
make
cd ..
```
