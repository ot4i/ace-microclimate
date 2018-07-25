# Demonstration

## Deploy Helm chart via Microclimate
1. Trigger build from Microclimate

## Test Deployment
2. Check deployment and service in ICP, note down NodePort for the ACE Server.

3. Open ACE Web UI and show deployed flow

4. POST to the Transformation Map flow REST API:
~~~
$ curl -X POST http://<ICP proxy IP>:<ACE Server NodePort>/Transformation_Map --data @Input_TransformationMap.xml
~~~
with Input_TransformationMap.xml as payload.

5. POST to the Temperature Converter flow REST API:
~~~
$ curl -X POST http://<ICP proxy IP>:<ACE Server NodePort>/TemperatureConverter/TemperatureConverter --data @Input_TemperatureConverter.xml
~~~
with Input_TransformationMap.xml as payload.

6. Get Ben's Simple Test REST API:
~~~
$ curl -X GET http://<ICP proxy IP>:<ACE Server NodePort>/benssimplerestapi/v1/object
~~~

Note: Steps 4, 5, and 6 can also be executed in Postman, using the collection in this folder.

## Make change to code
Make a simple change to the code:

7. For example, in `ace-pi/BensSimpleRESTAPI/getObject_Compute.esql` change the code FROM
~~~
SET OutputRoot.JSON.Data.Output.VersionOfThisRESTAPI = '1';
SET OutputRoot.JSON.Data.Output.WhoIsGoingToWinTheWorldCup = 'Brazil';
~~~
TO
~~~
SET OutputRoot.JSON.Data.Output.VersionOfThisRESTAPI = '2';
SET OutputRoot.JSON.Data.Output.WhoIsGoingToWinTheWorldCup = 'France';
~~~

## Redeploy Helm chart via Microclimate
8. Trigger build from Microclimate

## Test the change
9. Await for successful deployment.

10. Get Ben's Simple Test REST API (NodePort does not change):
~~~
$ curl -X GET http://<ICP proxy IP>:<ACE Server NodePort>/benssimplerestapi/v1/object
~~~
