#### <a name="configurando-java"></a> Java

```
# You can use any Docker image from Docker Hub or your own container registry
image: maven:3.3.3

pipelines:
  default:
    - step:
        script:  # Modify the commands below to build and test your repository.
          - mvn --version
          - mvn clean install
```
