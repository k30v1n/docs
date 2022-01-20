## How to run specific docker step

To run specific docker steps we can run the following commands

```
docker build -t image-tag:test --target=test . 
docker run image-tag:test
docker build -t temp-test:test --target=test . & docker run temp-test:test
```