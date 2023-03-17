# Week 2 — Distributed Tracing

Create a account on Honeycomb
Grab the API key from your honeycomb account:
```
export HONEYCOMB_API_KEY=""
export HONEYCOMB_SERVICE_NAME="Cruddur"
gp env HONEYCOMB_API_KEY=""
gp env HONEYCOMB_SERVICE_NAME="Cruddur"
```
To check
```
env | grep HONEY
```
```
pip install opentelemetry-api
cd backend-flask/
```
Add the following files to our requirements.txt
```
opentelemetry-api 
opentelemetry-sdk 
opentelemetry-exporter-otlp-proto-http 
opentelemetry-instrumentation-flask 
opentelemetry-instrumentation-requests
```
```
pip install -r requirements.txt
```

Add the following code to the app.py
```
# Honeycomb
from opentelemetry import trace
from opentelemetry.instrumentation.flask import FlaskInstrumentor
from opentelemetry.instrumentation.requests import RequestsInstrumentor
from opentelemetry.exporter.otlp.proto.http.trace_exporter import OTLPSpanExporter
from opentelemetry.sdk.trace import TracerProvider
from opentelemetry.sdk.trace.export import BatchSpanProcessor

# Initialize tracing and an exporter that can send data to Honeycomb
provider = TracerProvider()
processor = BatchSpanProcessor(OTLPSpanExporter())
provider.add_span_processor(processor)
trace.set_tracer_provider(provider)
tracer = trace.get_tracer(__name__)

app = Flask(__name__)
# Initialize automatic instrumentation with Flask
FlaskInstrumentor().instrument_app(app)
RequestsInstrumentor().instrument()
```

Add the following Env Vars to backend-flask in docker compose
```
 OTEL_SERVICE_NAME: "backend-flask"
 OTEL_EXPORTER_OTLP_ENDPOINT: "https://api.honeycomb.io"
 OTEL_EXPORTER_OTLP_HEADERS: "x-honeycomb-team=${HONEYCOMB_API_KEY}"
```
On docker compose-up, we can see the data successfully sent to Honeycomb
<img width="925" alt="image" src="https://user-images.githubusercontent.com/77580311/224369800-97f1f0c1-50d7-48d4-95ba-360aa251874b.png">


# X-Ray
Add this to the requirements.txt
```
aws-xray-sdk
```
Run the following commands to install dependencies
```
cd backend-flask/
pip install -r requirements.txt
```
Add to app.py
```
# x-ray
from aws_xray_sdk.core import xray_recorder
from aws_xray_sdk.ext.flask.middleware import XRayMiddleware

xray_url = os.getenv("AWS_XRAY_URL")
xray_recorder.configure(service='backend-flask', dynamic_naming=xray_url)

XRayMiddleware(app, xray_recorder)
```
Add aws/json/xray.json
```
{
    "SamplingRule": {
        "RuleName": "Cruddur",
        "ResourceARN": "*",
        "Priority": 9000,
        "FixedRate": 0.1,
        "ReservoirSize": 5,
        "ServiceName": "backend-flask",
        "ServiceType": "*",
        "Host": "*",
        "HTTPMethod": "*",
        "URLPath": "*",
        "Version": 1
    }
}
```
Run the command
```
aws xray create-group --group-name "Cruddur" --filter-expression "service(\"backend-flask\")"
aws xray create-sampling-rule --cli-input-json file://aws/json/xray.json
```

Add Daemon Service to Docker Compose
```
  xray-daemon:
    image: "amazon/aws-xray-daemon"
    environment:
      AWS_ACCESS_KEY_ID: "${AWS_ACCESS_KEY_ID}"
      AWS_SECRET_ACCESS_KEY: "${AWS_SECRET_ACCESS_KEY}"
      AWS_REGION: "us-east-1"
    command:
      - "xray -o -b xray-daemon:2000"
    ports:
      - 2000:2000/udp
```
Add these two env vars to our backend-flask in our docker-compose.yml file
```
     AWS_XRAY_URL: "*4567-${GITPOD_WORKSPACE_ID}.${GITPOD_WORKSPACE_CLUSTER_HOST}*"
     AWS_XRAY_DAEMON_ADDRESS: "xray-daemon:2000"
```
On docker compose-up, we can see the data successfully sent to X-ray
<img width="956" alt="image" src="https://user-images.githubusercontent.com/77580311/224368600-a9b96d6a-bb41-4c09-9b79-89069d8d3183.png">

<img width="863" alt="image" src="https://user-images.githubusercontent.com/77580311/224368942-825da269-54e8-411a-9a30-8b0c6c96b253.png">

Add segments and subsegments to backend-flask/services/user_activities.py
```
 from aws_xray_sdk.core import xray_recorder

 # xray 
 segment = xray_recorder.begin_segment('user_activities')
 
  subsegment = xray_recorder.begin_subsegment('mock-data')
  # xray ---
  dict = {
     "now": now.isoformat(),
     "results-size": len(model['data'])
  }
  subsegment.put_metadata('key', dict, 'namespace')
```
# CloudWatch Logs
Add to requirements.txt
```
watchtower
```
```
cd backend-flask/
pip install -r requirements.txt
```
In app.py
```
# CloudWatch Logs ----
import watchtower
import logging
from time import strftime


# Configuring Logger to Use CloudWatch
LOGGER = logging.getLogger(__name__)
LOGGER.setLevel(logging.DEBUG)
console_handler = logging.StreamHandler()
cw_handler = watchtower.CloudWatchLogHandler(log_group='cruddur')
LOGGER.addHandler(console_handler)
LOGGER.addHandler(cw_handler)
LOGGER.info("test log")


@app.after_request
def after_request(response):
   timestamp = strftime('[%Y-%b-%d %H:%M]')
   LOGGER.error('%s %s %s %s %s %s', timestamp, request.remote_addr, request.method, request.scheme, request.full_path, response.status)
   return response
```
Add this to home_activities.py
```
LOGGER.info('Hello Cloudwatch! from  /api/activities/home')
```
Set the env var in your backend-flask for docker-compose.yml
```
      AWS_DEFAULT_REGION: "${AWS_DEFAULT_REGION}"
      AWS_ACCESS_KEY_ID: "${AWS_ACCESS_KEY_ID}"
      AWS_SECRET_ACCESS_KEY: "${AWS_SECRET_ACCESS_KEY}"
```




