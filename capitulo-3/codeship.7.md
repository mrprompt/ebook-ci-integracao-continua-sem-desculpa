#### <a name="configurando-ruby"></a> Ruby

```
# Tests
rvm use 2.2.0 --install
bundle install
```
```
# Pipeline
bundle exec jekyll build
bundle exec htmlproof --allow-hash-href --disable-external --empty-alt-ignore ./_site
```
