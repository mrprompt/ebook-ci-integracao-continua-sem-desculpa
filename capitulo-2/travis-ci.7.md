# <a name="configurando-ruby"></a> Ruby

Não possuo experiência com Ruby além de minúsculos projetos de exemplo e alguns sites hospedados no **GitHub**, que
utilizam o **Jekyll** como base. Neste exemplo, mostro como rodar um projeto em **Jekyll** hospedado no próprio
**GitHub**. Nele, rodo o build do **Jekyll** e o **HtmlProofer**, para analisar links e etc. Porém, rodo somente
no branch **master** os testes.

```
language: ruby
rvm:
- 2.1

# Assume bundler is being used, therefore the `install` step will run `bundle install` by default.
script:
    - bundle exec jekyll build
    - bundle exec htmlproof --allow-hash-href --disable-external --empty-alt-ignore ./_site

# branch whitelist, only for GitHub Pages
branches:
  only:
  - master

env:
  global:
  - NOKOGIRI_USE_SYSTEM_LIBRARIES=true # speeds up installation of html-proofer
```
