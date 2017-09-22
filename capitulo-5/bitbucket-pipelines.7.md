#### <a name="configurando-ruby"></a> Ruby

```
image: ruby:2.3.0

pipelines:
  default:
    - step:
        script:  # Modify the commands below to build and test your repository.
          - ruby --version
          - bundler --version
          - bundle install
```
