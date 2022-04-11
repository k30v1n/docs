# How to run performance test with locust

LOCUST is a performance test tool that runs using python.
https://locust.io/

An example of locust test:

```python
from locust import HttpUser, between, task


class WebsiteUser(HttpUser):
    wait_time = between(5, 15)
    
    def on_start(self):
        self.client.post("/login", {
            "username": "test_user",
            "password": ""
        })
    
    @task
    def index(self):
        self.client.get("/")
        self.client.get("/static/assets.js")
        
    @task
    def about(self):
        self.client.get("/about/")
```


My own example repository https://github.com/k30v1n/locust 