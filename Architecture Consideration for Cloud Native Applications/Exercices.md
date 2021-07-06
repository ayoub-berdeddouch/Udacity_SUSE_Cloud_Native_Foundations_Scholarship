### Flask App : Python-HelloWorld


```python

from flask import Flask

app = Flask(__name__)


@app.route("/")
def hello():

    return "Hello World this is me Ayoub!"


if __name__ == "__main__":

    
    
    app.run(host='0.0.0.0') # or 127.0.0.1 or localhost
    

```

### Requirments 

>Flask==1.1.1
>werkzeug==0.16.1


### Run

> python app.py 
 or 
> python3 app.py



### TODO 

```
Exercise
Extend the Python Flask application with /status and /metrics endpoints, considering the following requirements:

* Both endpoints should return an HTTP 200 status code
* Both endpoints should return a JSON response e.g. {"user": "admin"}. (Note: the JSON response can be hardcoded at this stage)
* The __/status__ endpoint should return a response similar to this example: 
	> result: OK - healthy
* The __/metrics__ endpoint should return a response similar to this example: 
	> data: {UserCount: 140, UserCountActive: 23}
	
```



### Solution


```python

from flask import Flask
from flask import json
import logging

app = Flask(__name__)

@app.route('/status')
def healthcheck():
    response = app.response_class(
            response  = json.dumps({"result":"OK - healthy"}),
            status = 200,
            mimetype = 'application/json'
    )
    # log line
    app.logger.info('Status Request successfull')

    return response

@app.route('/metrics')
def metrics():
    response = app.response_class(
        response = json.dumps({"status":"success","code":0,"data":{"UserCount":140, "UserCountActive":23}}),
        status = 200,
        mimetype = "application/json"

    )
    # log line
    app.logger.info('Metrics Request successfull')

    return response

@app.route("/")
def hello():

    # log line
    app.logger.info('Welcome Request successfull')

    return "Hello World this is me Ayoub!"


if __name__ == "__main__":

    ## stream logs to app.log file
    logging.basicConfig(filename='app.log',level=logging.DEBUG)
    
    #app.run(host='127.0.0.1')
    app.run(host='127.0.0.1', port=80 ,debug=True)


```

### Run

> python app.py 
 or 
> python3 app.py




```logs
INFO:werkzeug: * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
INFO:werkzeug: * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
INFO:werkzeug: * Running on http://0.0.0.0:80/ (Press CTRL+C to quit)
INFO:werkzeug: * Restarting with windowsapi reloader
WARNING:werkzeug: * Debugger is active!
INFO:werkzeug: * Debugger PIN: 293-211-000
INFO:werkzeug: * Running on http://127.0.0.1:80/ (Press CTRL+C to quit)
INFO:app:Welcome Request successfull
INFO:werkzeug:127.0.0.1 - - [17/Jun/2021 18:32:29] "[37mGET / HTTP/1.1[0m" 200 -
INFO:werkzeug:127.0.0.1 - - [17/Jun/2021 18:32:30] "[33mGET /favicon.ico HTTP/1.1[0m" 404 -
INFO:werkzeug:127.0.0.1 - - [17/Jun/2021 18:32:35] "[33mGET /static HTTP/1.1[0m" 404 -
INFO:app:Metrics Request successfull
INFO:werkzeug:127.0.0.1 - - [17/Jun/2021 18:32:41] "[37mGET /metrics HTTP/1.1[0m" 200 -
INFO:werkzeug:127.0.0.1 - - [17/Jun/2021 18:32:45] "[33mGET /health HTTP/1.1[0m" 404 -
INFO:app:Status Request successfull
INFO:werkzeug:127.0.0.1 - - [17/Jun/2021 18:32:55] "[37mGET /status HTTP/1.1[0m" 200 -
```
