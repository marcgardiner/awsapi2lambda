Let's test our API using curl:

	curl -X GET -H "Content-Type: application/json" -H "X-API-key: some_api_key" INVOKE_URL/collection/SOME_RANDOM_ID/items
	{"code": 200, "results": "A nice API"}

Let's have a look at the CloudWatch logs. Among other things, we can see:

	Launched with event:
	{
	    "body": {},
	    "headers": {
	        "Content-Type": "application/json",
	        "Via": "*********",
	        "CloudFront-Is-Desktop-Viewer": "true",
	        "CloudFront-Is-SmartTV-Viewer": "false",
	        "CloudFront-Forwarded-Proto": "https",
	        "X-Forwarded-For": "******, ******",
	        "CloudFront-Viewer-Country": "BE",
	        "Accept": "*/*",
	        "User-Agent": "curl/7.51.0",
	        "X-Amzn-Trace-Id": "Root=******",
	        "Host": "******.execute-api.eu-west-1.amazonaws.com",
	        "X-Forwarded-Proto": "https",
	        "X-Amz-Cf-Id": "******",
	        "CloudFront-Is-Tablet-Viewer": "false",
	        "X-Forwarded-Port": "443",
	        "X-API-key": "some_api_key",
	        "CloudFront-Is-Mobile-Viewer": "false"
	    },
	    "params": {
	        "collectionId": "SOME_RANDOM_ID"
	    },
	    "method": "GET",
	    "query": {}
	}

Now I replace the content of the example.yml file by the content of the second_example.yml . In second_example.yml I remove the requestTemplates from the methods definitions.
I then commit the changes. I push them to the repo. It triggers the Pipeline and I wait for the API to be deployed again.

When I test the API again using curl, it gives me the same result as previously in the CloudWatch logs:

	Launched with event:
	{
	    "body": {},
	    "headers": {
	        "Content-Type": "application/json",
	        "Via": "*********",
	        "CloudFront-Is-Desktop-Viewer": "true",
	        "CloudFront-Is-SmartTV-Viewer": "false",
	        "CloudFront-Forwarded-Proto": "https",
	        "X-Forwarded-For": "******, ******",
	        "CloudFront-Viewer-Country": "BE",
	        "Accept": "*/*",
	        "User-Agent": "curl/7.51.0",
	        "X-Amzn-Trace-Id": "Root=******",
	        "Host": "******.execute-api.eu-west-1.amazonaws.com",
	        "X-Forwarded-Proto": "https",
	        "X-Amz-Cf-Id": "******",
	        "CloudFront-Is-Tablet-Viewer": "false",
	        "X-Forwarded-Port": "443",
	        "X-API-key": "some_api_key",
	        "CloudFront-Is-Mobile-Viewer": "false"
	    },
	    "params": {
	        "collectionId": "SOME_RANDOM_ID"
	    },
	    "method": "GET",
	    "query": {}
	}

The expected result is:

	Launched with event:
	{
	}

since I removed the requestTemplates from the method definitions in the API. This means that the API definition is not updated from one Pipeline execution to the other.
