--- 

title: Subtl Web API 

language_tabs: 
   - shell
   - python
   - javascript
   - java

toc_footers: 
   - <a href='#'>Sign Up for a Developer Key</a> 
   - <a href='https://github.com/lavkumarv'>Documentation Powered by lav</a> 

includes: 
   - errors 


--- 


# Getting Started

## Basics 
Firt, create a workspace by using the `/api_v2/workspace` endpoint. 

Create a library using `/api_v2/workspace/{workspace_id}/add_library` . With this library ID, you can upload documents to 
this library by sending your documents to `/api_v2/library/{library_id}/file` endpoint. 

Once you have added all the documents, you can create a transaction by using the `/api_v2/library/{library_id}/transaction` endpoint,
containing the generated answer to the question you had, using the documents you uploaded. 

That's simple, isn't it?

For full details on the available APIs and their options visit the api reference.

## Authentication
Some APIs of `subtl` uses an Bearer Authentication for authenticating requests. This is required to secure the API calls. Add an http header in the following form to your requests.

authorization: Bearer <your_api_key>

You can request an API key from us. 

# Concepts 

## Workspace 
In `subtl.ai`, we define the workspace as an single indepedent thread for 

## Library 
Libraries represents a collection, wherence for each workspace, the library stores the transactions and documents.
In a sense, the workspace represents the metadata for the thread, while the library represents the main content of the 
thread. 

## Document
Documents represents the chunks that are used to provide context to an LLM and reduce the chance of hallucination
to the LLM. These chunks 

## Transaction
Transactions are used to denote the retrieval augmented generations that are performed when a user queries in a library.
Each transaction contains a query, generated answer and the library it belongs to. Transactions 


# Tutorial 

This tutorial will walk you through the basics for using Subtl API for your project.

## Step 1 : API Key

You can easily get an API key by requesting any of us for same. 

## Step 2 : Create Workspace

To work with your documents privately, you should create a workspace. This can be done by using sending a POST request to `/api_v2/workspace`

The python code shown here does it. It creates a workspace named, `work` with `free_tier` subscription for now. 

You can reuse a workspace once it is created. 

```python 
import requests
import json

url = "http://localhost/api_v2/workspace/"
headers = {
    "accept": "application/json",
    "Content-Type": "application/json"
}
data = {
    "name": "work",
    "max_threshold": -1,
    "is_public": False,
    "is_default": False,
    "subscription_slug": "free_tier"
}

response = requests.post(url, headers=headers, data=json.dumps(data)).json()

workspace_id = response["workspace"]["id"],

print(f"Workspace ID : {workspace_id}")

```

## Step 3 : Create Library
 
Once you have created a workspace, you can use it to create a library for the same workspace. 
The library can be created by using the POST request to `/api_v2/workspace/{workspace_id}/add_library` endpoint. 

It returns a JSON, from which the Python code shows how to extract the Library ID.


```python
import requests
import json

url = 'http://localhost/api_v2/workspace/{workspace_id}/add_library'
headers = {
    'accept': 'application/json',
    'Content-Type': 'application/json'
}
data = {
    "name": "string",
    "desc": "",
    "public": True,
    "default_contribute": True
}

response = requests.post(url, headers=headers, data=json.dumps(data)).json()

# Get the library ID
print(f"Library ID: {response['library']['group']['id']}")
```

## Step 4 : Add Documents 

Adding documents is very easy in `subtl.ai`. Once you have created a library, we can upload documents to it by using the `/api_v2/library/{library_id}/file` endpoint.
We will pass the file to this API and it returns a JSON which confirms that we have uploaded the document to the library.

```python
import requests

url = 'http://localhost/api_v2/library/{library_id}/file'
headers = {
    'accept': 'application/json'
}
files = {
    'file': open('openapi.yaml', 'rb') # Add any file 
}

response = requests.post(url, headers=headers, files=files)

# Print response 
print(response.json())
```

## Step 5 : Querying the Documents 

Once all documents are uploaded to a library, you can finally perform querying on the documents by using the `/api_v2/library/{library_id}/transaction`
method. 


```python

import requests
import json

url = 'http://localhost/api_v2/library/{library_id}/transaction'
headers = {
    'accept': 'application/json',
    'Content-Type': 'application/json'
}
data = {
    "query_string": "{your_question_here}",
    "transaction_ids": [],
    "agent_persona": "Your name is Subtl Bot. You are an AI assistant designed by researchers and engineers of Subtl.ai to help users based on private knowledge."
}

response = requests.post(url, headers=headers, data=json.dumps(data)).json()

# Print fetched answer
print(f"Answer generated : {response['generated_answer']}")
```

## That's it 
This means, you are now ready to use the subtl API for your project!

# API Docs 

The following describes the APIs offered by Subtl over the public domain:


# Account API 

## Get Current Account

> Example Usage:

```python
import requests

url = "http://localhost/api_v2/account/me"
headers = {
    "accept": "application/json"
}

response = requests.get(url, headers=headers)
print(response.json())

```

```shell
curl -X 'GET' \
  'http://localhost/api_v2/account/me' \
  -H 'accept: application/json'
```

```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;

public class Main {
    public static void main(String[] args) {
        try {
            String url = "http://localhost/api_v2/account/me";
            URL obj = new URL(url);
            HttpURLConnection con = (HttpURLConnection) obj.openConnection();
            
            // Set request method to GET
            con.setRequestMethod("GET");
            con.setRequestProperty("Accept", "application/json");

            // Get the response
            int responseCode = con.getResponseCode();
            if (responseCode == HttpURLConnection.HTTP_OK) {
                BufferedReader in = new BufferedReader(new InputStreamReader(con.getInputStream()));
                String inputLine;
                StringBuffer response = new StringBuffer();

                while ((inputLine = in.readLine()) != null) {
                    response.append(inputLine);
                }
                in.close();
                
                // Print result
                System.out.println(response.toString());
            } else {
                System.out.println("GET request failed. Response Code: " + responseCode);
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

```

```javascript
const url = 'http://localhost/api_v2/account/me';

fetch(url, {
  method: 'GET',
  headers: {
    'Accept': 'application/json'
  }
})
  .then(response => {
    if (!response.ok) {
      throw new Error('Network response was not ok ' + response.statusText);
    }
    return response.json();
  })
  .then(data => console.log(data))
  .catch(error => console.error('There was a problem with the fetch operation:', error));

```

> The above request, on a success, returns JSON structured like this:

```json
{
  "email": "string",
  "email_verified": false,
  "given_name": "string",
  "family_name": "string",
  "picture": "string",
  "id": "string"
}
```


**Description**: This API allows you to retrieve the details of the current user account, including basic profile information such as email, name, picture, and account verification status.

### HTTP Request 
***GET*** request on `/api_v2/account/me`



**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |




## Updating Current Account

> Example Usage:


```python
import requests
import json

url = "http://localhost/api_v2/account/me"
headers = {
    "accept": "application/json",
    "Content-Type": "application/json"
}
data = {
    "email": "string",
    "email_verified": True,
    "given_name": "string",
    "family_name": "string",
    "picture": "string"
}

response = requests.patch(url, headers=headers, data=json.dumps(data))
print(response.json())


```

```shell
curl -X 'PATCH' \
  'http://localhost/api_v2/account/me' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "email": "string",
  "email_verified": true,
  "given_name": "string",
  "family_name": "string",
  "picture": "string"
}'
```

```java
import java.io.OutputStream;
import java.net.HttpURLConnection;
import java.net.URL;

public class Main {
    public static void main(String[] args) {
        try {
            String url = "http://localhost/api_v2/account/me";
            URL obj = new URL(url);
            HttpURLConnection con = (HttpURLConnection) obj.openConnection();

            // Set request method to PATCH
            con.setRequestMethod("PATCH");
            con.setRequestProperty("Accept", "application/json");
            con.setRequestProperty("Content-Type", "application/json");

            // JSON payload
            String jsonInputString = "{\"email\": \"string\", \"email_verified\": true, \"given_name\": \"string\", \"family_name\": \"string\", \"picture\": \"string\"}";

            // Enable input/output streams
            con.setDoOutput(true);
            try(OutputStream os = con.getOutputStream()) {
                byte[] input = jsonInputString.getBytes("utf-8");
                os.write(input, 0, input.length);           
            }

            // Get response
            int responseCode = con.getResponseCode();
            System.out.println("Response Code : " + responseCode);
            if (responseCode == HttpURLConnection.HTTP_OK) {
                BufferedReader in = new BufferedReader(new InputStreamReader(con.getInputStream()));
                String inputLine;
                StringBuffer response = new StringBuffer();
                while ((inputLine = in.readLine()) != null) {
                    response.append(inputLine);
                }
                in.close();
                System.out.println(response.toString());
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}


```

```javascript
const url = 'http://localhost/api_v2/account/me';
const data = {
  email: "string",
  email_verified: true,
  given_name: "string",
  family_name: "string",
  picture: "string"
};

fetch(url, {
  method: 'PATCH',
  headers: {
    'Accept': 'application/json',
    'Content-Type': 'application/json'
  },
  body: JSON.stringify(data)
})
  .then(response => {
    if (!response.ok) {
      throw new Error('Network response was not ok ' + response.statusText);
    }
    return response.json();
  })
  .then(data => console.log(data))
  .catch(error => console.error('There was a problem with the fetch operation:', error));

```

> The above request, on sucess, returns JSON structured like this:

```json
{
  "email": "string",
  "email_verified": false,
  "given_name": "string",
  "family_name": "string",
  "picture": "string",
  "id": "string"
}
```

**Description** : This API allows the current user to update their account details, such as email, name, profile picture, and email verification status.

### HTTP Request 
***PATCH*** request on `/api_v2/account/me` 


**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 422 | Validation Error |




# Workspace API



## Creates Workspace

> Example Usage: 

```python
import requests
import json

url = "http://localhost/api_v2/workspace/"
headers = {
    "accept": "application/json",
    "Content-Type": "application/json"
}
data = {
    "name": "string",
    "max_threshold": -1,
    "is_public": False,
    "is_default": False,
    "subscription_slug": "free_tier"
}

response = requests.post(url, headers=headers, data=json.dumps(data))
print(response.json())

```

```java
import java.io.BufferedReader;
import java.io.DataOutputStream;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;

public class Main {
    public static void main(String[] args) {
        try {
            String url = "http://localhost/api_v2/workspace/";
            URL obj = new URL(url);
            HttpURLConnection con = (HttpURLConnection) obj.openConnection();
            
            // Set request method to POST
            con.setRequestMethod("POST");
            con.setRequestProperty("Accept", "application/json");
            con.setRequestProperty("Content-Type", "application/json");

            // JSON payload
            String jsonInputString = "{ \"name\": \"string\", \"max_threshold\": -1, \"is_public\": false, \"is_default\": false, \"subscription_slug\": \"free_tier\" }";

            // Send post request
            con.setDoOutput(true);
            try (DataOutputStream wr = new DataOutputStream(con.getOutputStream())) {
                wr.writeBytes(jsonInputString);
                wr.flush();
            }

            // Get the response code
            int responseCode = con.getResponseCode();
            System.out.println("Response Code: " + responseCode);
            
            if (responseCode == HttpURLConnection.HTTP_OK) {
                BufferedReader in = new BufferedReader(new InputStreamReader(con.getInputStream()));
                String inputLine;
                StringBuffer response = new StringBuffer();

                while ((inputLine = in.readLine()) != null) {
                    response.append(inputLine);
                }
                in.close();
                
                // Print result
                System.out.println(response.toString());
            } else {
                System.out.println("POST request failed. Response Code: " + responseCode);
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

```

```javascript
const url = 'http://localhost/api_v2/workspace/';
const data = {
  name: "string",
  max_threshold: -1,
  is_public: false,
  is_default: false,
  subscription_slug: "free_tier"
};

fetch(url, {
  method: 'POST',
  headers: {
    'Accept': 'application/json',
    'Content-Type': 'application/json'
  },
  body: JSON.stringify(data)
})
  .then(response => {
    if (!response.ok) {
      throw new Error('Network response was not ok ' + response.statusText);
    }
    return response.json();
  })
  .then(data => console.log(data))
  .catch(error => console.error('There was a problem with the fetch operation:', error));

```

```shell
curl -X 'POST' \
  'http://localhost/api_v2/workspace/' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "name": "string",
  "max_threshold": -1,
  "is_public": false,
  "is_default": false,
  "subscription_slug": "free_tier"
}'
```

> The above request, on success, returns JSON structured like this:

```json
{
  "workspace": {
    "name": "string",
    "max_threshold": 0,
    "is_public": true,
    "is_default": true,
    "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "libraries": [
      {
        "name": "string",
        "desc": "string",
        "public": true,
        "default_contribute": true,
        "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
        "workspace_id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
        "group": {
          "id": "string",
          "name": "string",
          "index_built": true,
          "index_loaded": true,
          "doc_processed_count": 0
        }
      }
    ]
  },
  "is_admin": true,
  "subscription": {
    "name": "string",
    "description": "string",
    "total_token_limit": 0,
    "allowed_questions_per_day": 0,
    "max_users": 0,
    "library_limit": 0,
    "price": 0,
    "additional_user_price": 0,
    "additional_user_questions_per_day": 0,
    "slug": "string",
    "workspace_id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "start_date": "2024-10-07T22:11:53.603Z",
    "end_date": "2024-10-07T22:11:53.603Z",
    "active": true
  }
}
```


**Summary:** This API allows the user to create a workspace. 

### HTTP Request 
***POST*** request on  `/api_v2/workspace/` 

**Responses**

| Code | Description |
| ---- | ----------- |
| 201 | Successful Response |
| 422 | Validation Error |



## Get My Workspaces

> Example Usage:

```python
import requests

url = "http://localhost/api_v2/workspace/"
headers = {
    "accept": "application/json"
}

response = requests.get(url, headers=headers)
print(response.json())

```

```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;

public class Main {
    public static void main(String[] args) {
        try {
            String url = "http://localhost/api_v2/workspace/";
            URL obj = new URL(url);
            HttpURLConnection con = (HttpURLConnection) obj.openConnection();
            
            // Set request method to GET
            con.setRequestMethod("GET");
            con.setRequestProperty("Accept", "application/json");

            // Get the response
            int responseCode = con.getResponseCode();
            if (responseCode == HttpURLConnection.HTTP_OK) {
                BufferedReader in = new BufferedReader(new InputStreamReader(con.getInputStream()));
                String inputLine;
                StringBuffer response = new StringBuffer();

                while ((inputLine = in.readLine()) != null) {
                    response.append(inputLine);
                }
                in.close();
                
                // Print result
                System.out.println(response.toString());
            } else {
                System.out.println("GET request failed. Response Code: " + responseCode);
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

```

```javascript
const url = 'http://localhost/api_v2/workspace/';

fetch(url, {
  method: 'GET',
  headers: {
    'Accept': 'application/json'
  }
})
  .then(response => {
    if (!response.ok) {
      throw new Error('Network response was not ok ' + response.statusText);
    }
    return response.json();
  })
  .then(data => console.log(data))
  .catch(error => console.error('There was a problem with the fetch operation:', error));

```

```shell
curl -X 'GET' \
  'http://localhost/api_v2/workspace/' \
  -H 'accept: application/json'
```

> The above request, on success, returns JSON structured like this:

```json
[
  {
    "workspace": {
      "name": "string",
      "max_threshold": 0,
      "is_public": true,
      "is_default": true,
      "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
    },
    "is_admin": true
  }
]
```

**Description:** Fetches the current workspaces of the user. This API returns an array of workspaces that the user 
belongs to.

### HTTP Request 
***GET*** request on `/api_v2/workspace/` 

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |

## Update Workspace

> Example Usage: 

```python
import requests
import json

url = "http://localhost/api_v2/workspace/{workspace_id}"
headers = {
    "accept": "application/json",
    "Content-Type": "application/json"
}
data = {
    "name": "string",
    "is_public": True,
    "max_threshold": 0
}

response = requests.patch(url, headers=headers, data=json.dumps(data))
print(response.json())

```

```java
import java.io.BufferedReader;
import java.io.DataOutputStream;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;

public class Main {
    public static void main(String[] args) {
        try {
            String url = "http://localhost/api_v2/workspace/{workspace_id}";
            URL obj = new URL(url);
            HttpURLConnection con = (HttpURLConnection) obj.openConnection();
            
            // Set request method to PATCH
            con.setRequestMethod("PATCH");
            con.setRequestProperty("Accept", "application/json");
            con.setRequestProperty("Content-Type", "application/json");

            // JSON payload
            String jsonInputString = "{ \"name\": \"string\", \"is_public\": true, \"max_threshold\": 0 }";

            // Send patch request
            con.setDoOutput(true);
            try (DataOutputStream wr = new DataOutputStream(con.getOutputStream())) {
                wr.writeBytes(jsonInputString);
                wr.flush();
            }

            // Get the response code
            int responseCode = con.getResponseCode();
            System.out.println("Response Code: " + responseCode);
            
            if (responseCode == HttpURLConnection.HTTP_OK) {
                BufferedReader in = new BufferedReader(new InputStreamReader(con.getInputStream()));
                String inputLine;
                StringBuilder response = new StringBuilder();

                while ((inputLine = in.readLine()) != null) {
                    response.append(inputLine);
                }
                in.close();
                
                // Print result
                System.out.println(response.toString());
            } else {
                System.out.println("PATCH request failed. Response Code: " + responseCode);
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

```

```javascript
const url = 'http://localhost/api_v2/workspace/{workspace_id}';
const data = {
  name: "string",
  is_public: true,
  max_threshold: 0
};

fetch(url, {
  method: 'PATCH',
  headers: {
    'Accept': 'application/json',
    'Content-Type': 'application/json'
  },
  body: JSON.stringify(data)
})
  .then(response => {
    if (!response.ok) {
      throw new Error('Network response was not ok ' + response.statusText);
    }
    return response.json();
  })
  .then(data => console.log(data))
  .catch(error => console.error('There was a problem with the fetch operation:', error));

```

```shell
curl -X 'PATCH' \
  'http://localhost/api_v2/{workspace_id}' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "name": "string",
  "is_public": true,
  "max_threshold": 0
}'
```

> The above request, on success, returns JSON structured like this:

```json
{
  "name": "string",
  "max_threshold": 0,
  "is_public": true,
  "is_default": true,
  "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
}
```

**Description:** This API is used to perform update on a workspace. 

### HTTP Request 
***PATCH*** request on `/api_v2/workspace/{workspace_id}` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| workspace_id | path |  | Yes |  |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 422 | Validation Error |

## Delete Workspace

> Example Usage: 

```python
import requests

url = "http://localhost/api_v2/{workspace_id}"
headers = {
    "accept": "application/json"
}

response = requests.delete(url, headers=headers)
print(response.status_code)
print(response.json())  # Optional: print response content if applicable

```

```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;

public class Main {
    public static void main(String[] args) {
        try {

            String url = "http://localhost/api_v2/{workspace_id}" ;
            URL obj = new URL(url);
            HttpURLConnection con = (HttpURLConnection) obj.openConnection();
            
            // Set request method to DELETE
            con.setRequestMethod("DELETE");
            con.setRequestProperty("Accept", "application/json");

            // Get the response code
            int responseCode = con.getResponseCode();
            System.out.println("Response Code: " + responseCode);
            
            if (responseCode == HttpURLConnection.HTTP_OK) {
                BufferedReader in = new BufferedReader(new InputStreamReader(con.getInputStream()));
                String inputLine;
                StringBuilder response = new StringBuilder();

                while ((inputLine = in.readLine()) != null) {
                    response.append(inputLine);
                }
                in.close();
                
                // Print result
                System.out.println(response.toString());
            } else {
                System.out.println("DELETE request failed. Response Code: " + responseCode);
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

```

```javascript
const workspaceId = 'workspace_id'; // Replace with the actual workspace ID
const url = `http://localhost/api_v2/${workspaceId}`;

fetch(url, {
  method: 'DELETE',
  headers: {
    'Accept': 'application/json'
  }
})
  .then(response => {
    if (!response.ok) {
      throw new Error('Network response was not ok ' + response.statusText);
    }
    return response.json(); // Optional: handle the response content if needed
  })
  .then(data => console.log(data))
  .catch(error => console.error('There was a problem with the fetch operation:', error));

```

```shell
curl -X 'DELETE' \
  'http://localhost/api_v2/{workspace_id}' \
  -H 'accept: application/json'
```

> The above request, on success, returns JSON structured like this:

```json
"string"
```

**Description:** Delete Workspace

### HTTP Request 
***DELETE*** request on `/api_v2/workspace/{workspace_id}` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| workspace_id | path |  | Yes |  |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 422 | Validation Error |

## Add User To Workspace

> Example Usage:

```python
import requests

url = "http://localhost/api_v2/workspace/123e4567-e89b-12d3-a456-426614174000/add_user?user_id={user_id}&is_admin=false"
headers = {
    "accept": "application/json"
}

response = requests.post(url, headers=headers)
print(response.json())

```

```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;

public class Main {
    public static void main(String[] args) {
        try {
            String url = "http://localhost/api_v2/workspace/123e4567-e89b-12d3-a456-426614174000/add_user?user_id={user_id}&is_admin=false";
            URL obj = new URL(url);
            HttpURLConnection con = (HttpURLConnection) obj.openConnection();
            
            con.setRequestMethod("POST");
            con.setRequestProperty("Accept", "application/json");

            int responseCode = con.getResponseCode();
            System.out.println("Response Code: " + responseCode);
            
            if (responseCode == HttpURLConnection.HTTP_OK) {
                BufferedReader in = new BufferedReader(new InputStreamReader(con.getInputStream()));
                String inputLine;
                StringBuilder response = new StringBuilder();

                while ((inputLine = in.readLine()) != null) {
                    response.append(inputLine);
                }
                in.close();
                
                System.out.println(response.toString());
            } else {
                System.out.println("POST request failed. Response Code: " + responseCode);
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

```

```javascript
const url = 'http://localhost/api_v2/workspace/123e4567-e89b-12d3-a456-426614174000/add_user?user_id={user_id}&is_admin=false';

fetch(url, {
  method: 'POST',
  headers: {
    'Accept': 'application/json'
  }
})
  .then(response => {
    if (!response.ok) {
      throw new Error('Network response was not ok ' + response.statusText);
    }
    return response.json();
  })
  .then(data => console.log(data))
  .catch(error => console.error('There was a problem with the fetch operation:', error));

```

```shell
curl -X 'POST' \
  'http://localhost/api_v2/workspace/123e4567-e89b-12d3-a456-426614174000/add_user?user_id=%7Buser_id%7D&is_admin=false' \
  -H 'accept: application/json' \
  -d ''
```

> The above request, on success, returns JSON structured like this:

```json
{
  "account": {
    "email": "string",
    "email_verified": false,
    "given_name": "string",
    "family_name": "string",
    "picture": "string",
    "id": "string"
  },
  "is_admin": true
}
```
**Description:** Add User

### HTTP Request 
***POST*** request on `/api_v2/workspace/{workspace_id}/add_user` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| workspace_id | path |  | Yes |  |
| user_id | query |  | Yes |  |
| is_admin | query |  | No |  |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 422 | Validation Error |

## Get Workspace Users

> Example Usage: 

```python
import requests

url = "http://localhost/api_v2/workspace/{workspace_id}/users"
headers = {
    "accept": "application/json"
}

response = requests.get(url, headers=headers)
print(response.json())

```

```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;

public class Main {
    public static void main(String[] args) {
        try {
            
            String url = "http://localhost/api_v2/workspace/{workspaceId}/users";
            URL obj = new URL(url);
            HttpURLConnection con = (HttpURLConnection) obj.openConnection();
            
            // Set request method to GET
            con.setRequestMethod("GET");
            con.setRequestProperty("Accept", "application/json");

            // Get the response
            int responseCode = con.getResponseCode();
            if (responseCode == HttpURLConnection.HTTP_OK) {
                BufferedReader in = new BufferedReader(new InputStreamReader(con.getInputStream()));
                String inputLine;
                StringBuilder response = new StringBuilder();

                while ((inputLine = in.readLine()) != null) {
                    response.append(inputLine);
                }
                in.close();
                
                // Print result
                System.out.println(response.toString());
            } else {
                System.out.println("GET request failed. Response Code: " + responseCode);
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

```

```javascript
const workspaceId = '123e4567-e89b-12d3-a456-426614174000'; // Replace with the actual workspace ID
const url = `http://localhost/api_v2/workspace/${workspaceId}/users`;

fetch(url, {
  method: 'GET',
  headers: {
    'Accept': 'application/json'
  }
})
  .then(response => {
    if (!response.ok) {
      throw new Error('Network response was not ok ' + response.statusText);
    }
    return response.json();
  })
  .then(data => console.log(data))
  .catch(error => console.error('There was a problem with the fetch operation:', error));

```

```shell
curl -X 'GET' \
  'http://localhost/api_v2/workspace/{workspace_id}/users' \
  -H 'accept: application/json'
```

> The above request, on success, returns JSON structured like this:

```json
[
  {
    "account": {
      "email": "string",
      "email_verified": false,
      "given_name": "string",
      "family_name": "string",
      "picture": "string",
      "id": "string"
    },
    "is_admin": true
  }
]
```

**Description:** Get Workspace Users

### HTTP Request 
***GET*** request on `/api_v2/workspace/{workspace_id}/users` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| workspace_id | path |  | Yes |  |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 422 | Validation Error |

## Get Workspace Libraries

> Example Usage: 

```python
import requests

url = 'http://localhost/api_v2/workspace/123e4567-e89b-12d3-a456-426614174000/libraries'
headers = {
    'accept': 'application/json'
}

response = requests.get(url, headers=headers)
print(response.json())

```

```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;

public class Main {
    public static void main(String[] args) {
        try {
            String url = "http://localhost/api_v2/workspace/123e4567-e89b-12d3-a456-426614174000/libraries";
            URL obj = new URL(url);
            HttpURLConnection con = (HttpURLConnection) obj.openConnection();
            
            con.setRequestMethod("GET");
            con.setRequestProperty("Accept", "application/json");

            int responseCode = con.getResponseCode();
            System.out.println("Response Code: " + responseCode);
            
            if (responseCode == HttpURLConnection.HTTP_OK) {
                BufferedReader in = new BufferedReader(new InputStreamReader(con.getInputStream()));
                String inputLine;
                StringBuilder response = new StringBuilder();

                while ((inputLine = in.readLine()) != null) {
                    response.append(inputLine);
                }
                in.close();
                
                System.out.println(response.toString());
            } else {
                System.out.println("GET request failed. Response Code: " + responseCode);
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

```

```javascript
const url = 'http://localhost/api_v2/workspace/123e4567-e89b-12d3-a456-426614174000/libraries';

fetch(url, {
  method: 'GET',
  headers: {
    'Accept': 'application/json'
  }
})
  .then(response => {
    if (!response.ok) {
      throw new Error('Network response was not ok ' + response.statusText);
    }
    return response.json();
  })
  .then(data => console.log(data))
  .catch(error => console.error('There was a problem with the fetch operation:', error));

```

```shell
curl -X 'GET' \
  'http://localhost/api_v2/workspace/123e4567-e89b-12d3-a456-426614174000/libraries' \
  -H 'accept: application/json'
```

> The above request, on success, returns JSON structured like this:

```json
[
  {
    "library": {
      "name": "string",
      "desc": "string",
      "public": true,
      "default_contribute": true,
      "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "workspace_id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "group": {
        "id": "string",
        "name": "string",
        "index_built": true,
        "index_loaded": true,
        "doc_processed_count": 0
      }
    },
    "is_admin": true,
    "can_upload": true,
    "is_expert": true
  }
]
```

**Description:** Get Workspace Libraries

### HTTP Request 
***GET*** request on `/api_v2/workspace/{workspace_id}/libraries` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| workspace_id | path |  | Yes |  |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 422 | Validation Error |

## Get Workspace Public Libraries

> Example Usage: 

```python
import requests

url = 'http://localhost/api_v2/workspace/123e4567-e89b-12d3-a456-426614174000/public_libraries'
headers = {
    'accept': 'application/json'
}

response = requests.get(url, headers=headers)
print(response.json())

```

```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;

public class Main {
    public static void main(String[] args) {
        try {
            String url = "http://localhost/api_v2/workspace/123e4567-e89b-12d3-a456-426614174000/public_libraries";
            URL obj = new URL(url);
            HttpURLConnection con = (HttpURLConnection) obj.openConnection();
            
            con.setRequestMethod("GET");
            con.setRequestProperty("Accept", "application/json");

            int responseCode = con.getResponseCode();
            System.out.println("Response Code: " + responseCode);
            
            if (responseCode == HttpURLConnection.HTTP_OK) {
                BufferedReader in = new BufferedReader(new InputStreamReader(con.getInputStream()));
                String inputLine;
                StringBuilder response = new StringBuilder();

                while ((inputLine = in.readLine()) != null) {
                    response.append(inputLine);
                }
                in.close();
                
                System.out.println(response.toString());
            } else {
                System.out.println("GET request failed. Response Code: " + responseCode);
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

```

```javascript
const url = 'http://localhost/api_v2/workspace/123e4567-e89b-12d3-a456-426614174000/public_libraries';

fetch(url, {
  method: 'GET',
  headers: {
    'Accept': 'application/json'
  }
})
  .then(response => {
    if (!response.ok) {
      throw new Error('Network response was not ok ' + response.statusText);
    }
    return response.json();
  })
  .then(data => console.log(data))
  .catch(error => console.error('There was a problem with the fetch operation:', error));

```

```shell
curl -X 'GET' \
  'http://localhost/api_v2/workspace/123e4567-e89b-12d3-a456-426614174000/public_libraries' \
  -H 'accept: application/json'
```

> The above request, on success, returns JSON structured like this:

```json
[
  {
    "name": "string",
    "desc": "string",
    "public": true,
    "default_contribute": true,
    "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "workspace_id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "group": {
      "id": "string",
      "name": "string",
      "index_built": true,
      "index_loaded": true,
      "doc_processed_count": 0
    }
  }
]
```
**Description:** Get Workspace Public Libraries

### HTTP Request 
***GET*** request on `/api_v2/workspace/{workspace_id}/public_libraries` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| workspace_id | path |  | Yes |  |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 422 | Validation Error |


# Library API

## Create Library

> Example Usage: 

```python
import requests
import json

url = 'http://localhost/api_v2/workspace/123e4567-e89b-12d3-a456-426614174000/add_library'
headers = {
    'accept': 'application/json',
    'Content-Type': 'application/json'
}
data = {
    "name": "string",
    "desc": "",
    "public": True,
    "default_contribute": True
}

response = requests.post(url, headers=headers, data=json.dumps(data))
print(response.json())

```

```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.io.OutputStream;
import java.net.HttpURLConnection;
import java.net.URL;

public class Main {
    public static void main(String[] args) {
        try {
            String url = "http://localhost/api_v2/workspace/123e4567-e89b-12d3-a456-426614174000/add_library";
            URL obj = new URL(url);
            HttpURLConnection con = (HttpURLConnection) obj.openConnection();
            
            con.setRequestMethod("POST");
            con.setRequestProperty("Accept", "application/json");
            con.setRequestProperty("Content-Type", "application/json");
            con.setDoOutput(true);
            
            String jsonInputString = "{\"name\": \"string\", \"desc\": \"\", \"public\": true, \"default_contribute\": true}";

            try (OutputStream os = con.getOutputStream()) {
                byte[] input = jsonInputString.getBytes("utf-8");
                os.write(input, 0, input.length);           
            }

            int responseCode = con.getResponseCode();
            System.out.println("Response Code: " + responseCode);
            
            if (responseCode == HttpURLConnection.HTTP_OK) {
                BufferedReader in = new BufferedReader(new InputStreamReader(con.getInputStream()));
                String inputLine;
                StringBuilder response = new StringBuilder();

                while ((inputLine = in.readLine()) != null) {
                    response.append(inputLine);
                }
                in.close();
                
                System.out.println(response.toString());
            } else {
                System.out.println("POST request failed. Response Code: " + responseCode);
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

```

```javascript
const url = 'http://localhost/api_v2/workspace/123e4567-e89b-12d3-a456-426614174000/add_library';

const data = {
  name: "string",
  desc: "",
  public: true,
  default_contribute: true
};

fetch(url, {
  method: 'POST',
  headers: {
    'Accept': 'application/json',
    'Content-Type': 'application/json'
  },
  body: JSON.stringify(data)
})
  .then(response => {
    if (!response.ok) {
      throw new Error('Network response was not ok ' + response.statusText);
    }
    return response.json();
  })
  .then(data => console.log(data))
  .catch(error => console.error('There was a problem with the fetch operation:', error));

```

```shell
curl -X 'POST' \
  'http://localhost/api_v2/workspace/123e4567-e89b-12d3-a456-426614174000/add_library' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "name": "string",
  "desc": "",
  "public": true,
  "default_contribute": true
}'
```

> The above request, on success, returns JSON structured like this:

```json
{
  "library": {
    "name": "string",
    "desc": "string",
    "public": true,
    "default_contribute": true,
    "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "workspace_id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "group": {
      "id": "string",
      "name": "string",
      "index_built": true,
      "index_loaded": true,
      "doc_processed_count": 0
    }
  },
  "is_admin": true,
  "can_upload": true,
  "is_expert": true
}
```

**Description:** Create New Library

### HTTP Request 
***POST*** request on `/api_v2/workspace/{workspace_id}/add_library` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| workspace_id | path |  | Yes |  |

**Responses**

| Code | Description |
| ---- | ----------- |
| 201 | Successful Response |
| 422 | Validation Error |

## Update Library

> Example Usage: 

```python
import requests
import json

url = 'http://localhost/api_v2/library/123e4567-e89b-12d3-a456-426614174000'
headers = {
    'accept': 'application/json',
    'Content-Type': 'application/json'
}
data = {
    "name": "string",
    "desc": "string",
    "public": True,
    "default_contribute": True
}

response = requests.patch(url, headers=headers, data=json.dumps(data))
print(response.json())

```

```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.io.OutputStream;
import java.net.HttpURLConnection;
import java.net.URL;

public class Main {
    public static void main(String[] args) {
        try {
            String url = "http://localhost/api_v2/library/123e4567-e89b-12d3-a456-426614174000";
            URL obj = new URL(url);
            HttpURLConnection con = (HttpURLConnection) obj.openConnection();
            
            con.setRequestMethod("PATCH");
            con.setRequestProperty("Accept", "application/json");
            con.setRequestProperty("Content-Type", "application/json");
            con.setDoOutput(true); // Enable output to send a body

            String jsonInputString = "{\"name\": \"string\", \"desc\": \"string\", \"public\": true, \"default_contribute\": true}";

            try (OutputStream os = con.getOutputStream()) {
                byte[] input = jsonInputString.getBytes("utf-8");
                os.write(input, 0, input.length);           
            }

            int responseCode = con.getResponseCode();
            System.out.println("Response Code: " + responseCode);
            
            if (responseCode == HttpURLConnection.HTTP_OK) {
                BufferedReader in = new BufferedReader(new InputStreamReader(con.getInputStream()));
                String inputLine;
                StringBuilder response = new StringBuilder();

                while ((inputLine = in.readLine()) != null) {
                    response.append(inputLine);
                }
                in.close();
                
                System.out.println(response.toString());
            } else {
                System.out.println("PATCH request failed. Response Code: " + responseCode);
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

```

```javascript
const url = 'http://localhost/api_v2/library/123e4567-e89b-12d3-a456-426614174000';

const data = {
  name: "string",
  desc: "string",
  public: true,
  default_contribute: true
};

fetch(url, {
  method: 'PATCH',
  headers: {
    'Accept': 'application/json',
    'Content-Type': 'application/json'
  },
  body: JSON.stringify(data)
})
  .then(response => {
    if (!response.ok) {
      throw new Error('Network response was not ok ' + response.statusText);
    }
    return response.json();
  })
  .then(data => console.log(data))
  .catch(error => console.error('There was a problem with the fetch operation:', error));

```

```shell
curl -X 'PATCH' \
  'http://localhost/api_v2/library/123e4567-e89b-12d3-a456-426614174000' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "name": "string",
  "desc": "string",
  "public": true,
  "default_contribute": true
}'
```

> The above request, on success, returns JSON structured like this:

```json
{
  "name": "string",
  "desc": "string",
  "public": true,
  "default_contribute": true,
  "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "workspace_id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "group": {
    "id": "string",
    "name": "string",
    "index_built": true,
    "index_loaded": true,
    "doc_processed_count": 0
  }
}
```

**Description:** Update Library Details

### HTTP Request 
***PATCH*** request on `/api_v2/library/{library_id}` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| library_id | path |  | Yes |  |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 422 | Validation Error |

## Delete Library

> Example Usage: 

```python
import requests

url = 'http://localhost/api_v2/library/123e4567-e89b-12d3-a456-426614174000?ignore_backend=false'
headers = {
    'accept': '*/*'
}

response = requests.delete(url, headers=headers)
print(response.status_code)

```

```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;

public class Main {
    public static void main(String[] args) {
        try {
            String url = "http://localhost/api_v2/library/123e4567-e89b-12d3-a456-426614174000?ignore_backend=false";
            URL obj = new URL(url);
            HttpURLConnection con = (HttpURLConnection) obj.openConnection();
            
            con.setRequestMethod("DELETE");
            con.setRequestProperty("Accept", "*/*");

            int responseCode = con.getResponseCode();
            System.out.println("Response Code: " + responseCode);
            
            if (responseCode == HttpURLConnection.HTTP_OK || responseCode == HttpURLConnection.HTTP_NO_CONTENT) {
                System.out.println("Library deleted successfully.");
            } else {
                System.out.println("DELETE request failed. Response Code: " + responseCode);
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

```

```javascript
const url = 'http://localhost/api_v2/library/123e4567-e89b-12d3-a456-426614174000?ignore_backend=false';

fetch(url, {
  method: 'DELETE',
  headers: {
    'Accept': '*/*'
  }
})
  .then(response => {
    if (!response.ok) {
      throw new Error('Network response was not ok ' + response.statusText);
    }
    console.log('Library deleted successfully.');
  })
  .catch(error => console.error('There was a problem with the fetch operation:', error));

```

```shell
curl -X 'DELETE' \
  'http://localhost/api_v2/library/123e4567-e89b-12d3-a456-426614174000?ignore_backend=false' \
  -H 'accept: */*'
```

> The above request, on success, returns JSON structured like this:

```json
"string"
```

**Description:** Delete Library By Id

### HTTP Request 
***DELETE*** request on `/api_v2/library/{library_id}` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| library_id | path |  | Yes |  |
| ignore_backend | query |  | No |  |

**Responses**

| Code | Description |
| ---- | ----------- |
| 204 | Successful Response |
| 422 | Validation Error |

## Get Library Users

> Example Usage: 

```python
import requests

url = 'http://localhost/api_v2/library/123e4567-e89b-12d3-a456-426614174000/users'
headers = {
    'accept': 'application/json'
}

response = requests.get(url, headers=headers)
print(response.json())

```

```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;

public class Main {
    public static void main(String[] args) {
        try {
            String url = "http://localhost/api_v2/library/123e4567-e89b-12d3-a456-426614174000/users";
            URL obj = new URL(url);
            HttpURLConnection con = (HttpURLConnection) obj.openConnection();
            
            con.setRequestMethod("GET");
            con.setRequestProperty("Accept", "application/json");

            int responseCode = con.getResponseCode();
            System.out.println("Response Code: " + responseCode);
            
            if (responseCode == HttpURLConnection.HTTP_OK) {
                BufferedReader in = new BufferedReader(new InputStreamReader(con.getInputStream()));
                String inputLine;
                StringBuilder response = new StringBuilder();

                while ((inputLine = in.readLine()) != null) {
                    response.append(inputLine);
                }
                in.close();
                
                System.out.println(response.toString());
            } else {
                System.out.println("GET request failed. Response Code: " + responseCode);
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

```

```javascript
const url = 'http://localhost/api_v2/library/123e4567-e89b-12d3-a456-426614174000/users';

fetch(url, {
  method: 'GET',
  headers: {
    'Accept': 'application/json'
  }
})
  .then(response => {
    if (!response.ok) {
      throw new Error('Network response was not ok ' + response.statusText);
    }
    return response.json();
  })
  .then(data => console.log(data))
  .catch(error => console.error('There was a problem with the fetch operation:', error));

```

```shell
curl -X 'GET' \
  'http://localhost/api_v2/library/123e4567-e89b-12d3-a456-426614174000/users' \
  -H 'accept: application/json'
```

> The above request, on success, returns JSON structured like this:

```json
[
  {
    "account": {
      "email": "string",
      "email_verified": false,
      "given_name": "string",
      "family_name": "string",
      "picture": "string",
      "id": "string"
    },
    "is_admin": true,
    "can_upload": true,
    "is_expert": true
  }
]
```

**Description:** Get Library Users

### HTTP Request 
***GET*** request on `/api_v2/library/{library_id}/users` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| library_id | path |  | Yes |  |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 422 | Validation Error |

## Create Link

> Example Usage: 

```python
import requests
import json

url = 'http://localhost/api_v2/library/123e4567-e89b-12d3-a456-426614174000/link'
headers = {
    'accept': 'application/json',
    'Content-Type': 'application/json'
}
data = {
    "url": "string"
}

response = requests.post(url, headers=headers, data=json.dumps(data))
print(response.json())

```

```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.io.OutputStream;
import java.net.HttpURLConnection;
import java.net.URL;

public class Main {
    public static void main(String[] args) {
        String url = "http://localhost/api_v2/library/123e4567-e89b-12d3-a456-426614174000/link";
        String jsonInputString = "{\"url\": \"string\"}";

        try {
            HttpURLConnection con = (HttpURLConnection) new URL(url).openConnection();
            con.setRequestMethod("POST");
            con.setRequestProperty("Accept", "application/json");
            con.setRequestProperty("Content-Type", "application/json");
            con.setDoOutput(true);

            try (OutputStream os = con.getOutputStream()) {
                byte[] input = jsonInputString.getBytes("utf-8");
                os.write(input, 0, input.length);
            }

            int responseCode = con.getResponseCode();
            System.out.println("Response Code: " + responseCode);

            if (responseCode == HttpURLConnection.HTTP_OK) {
                BufferedReader in = new BufferedReader(new InputStreamReader(con.getInputStream()));
                StringBuilder response = new StringBuilder();
                String inputLine;

                while ((inputLine = in.readLine()) != null) {
                    response.append(inputLine);
                }
                in.close();

                System.out.println(response.toString());
            } else {
                System.out.println("POST request failed. Response Code: " + responseCode);
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

```

```javascript
const url = 'http://localhost/api_v2/library/123e4567-e89b-12d3-a456-426614174000/link';
const data = {
  url: "string"
};

fetch(url, {
  method: 'POST',
  headers: {
    'Accept': 'application/json',
    'Content-Type': 'application/json'
  },
  body: JSON.stringify(data)
})
  .then(response => {
    if (!response.ok) {
      throw new Error('Network response was not ok ' + response.statusText);
    }
    return response.json();
  })
  .then(data => console.log(data))
  .catch(error => console.error('There was a problem with the fetch operation:', error));

```

```shell
curl -X 'POST' \
  'http://localhost/api_v2/library/123e4567-e89b-12d3-a456-426614174000/link' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "url": "string"
}'
```

**Description:** Create Link

### HTTP Request 
***POST*** request on `/api_v2/library/{library_id}/link` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| library_id | path |  | Yes |  |

**Responses**

| Code | Description |
| ---- | ----------- |
| 201 | Successful Response |
| 422 | Validation Error |

# Document API 

## Create Document

> Example Usage: 

```python
import requests

url = 'http://localhost/api_v2/library/123e4567-e89b-12d3-a456-426614174000/file'
headers = {
    'accept': 'application/json'
}
files = {
    'file': open('openapi.yaml', 'rb')
}

response = requests.post(url, headers=headers, files=files)
print(response.json())

```

```java
import java.io.BufferedReader;
import java.io.DataOutputStream;
import java.io.File;
import java.io.FileInputStream;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;

public class Main {
    public static void main(String[] args) {
        String url = "http://localhost/api_v2/library/123e4567-e89b-12d3-a456-426614174000/file";
        String boundary = "===Boundary===";
        String LINE_FEED = "\r\n";
        String filePath = "openapi.yaml";

        try {
            File file = new File(filePath);
            FileInputStream fileInputStream = new FileInputStream(file);
            HttpURLConnection con = (HttpURLConnection) new URL(url).openConnection();

            con.setDoOutput(true);
            con.setRequestMethod("POST");
            con.setRequestProperty("Accept", "application/json");
            con.setRequestProperty("Content-Type", "multipart/form-data; boundary=" + boundary);

            try (DataOutputStream dos = new DataOutputStream(con.getOutputStream())) {
                dos.writeBytes("--" + boundary + LINE_FEED);
                dos.writeBytes("Content-Disposition: form-data; name=\"file\"; filename=\"" + file.getName() + "\"" + LINE_FEED);
                dos.writeBytes("Content-Type: application/octet-stream" + LINE_FEED);
                dos.writeBytes(LINE_FEED);

                byte[] buffer = new byte[4096];
                int bytesRead;
                while ((bytesRead = fileInputStream.read(buffer)) != -1) {
                    dos.write(buffer, 0, bytesRead);
                }

                dos.writeBytes(LINE_FEED);
                dos.writeBytes("--" + boundary + "--" + LINE_FEED);
            }

            int responseCode = con.getResponseCode();
            System.out.println("Response Code: " + responseCode);

            if (responseCode == HttpURLConnection.HTTP_OK) {
                BufferedReader in = new BufferedReader(new InputStreamReader(con.getInputStream()));
                String inputLine;
                StringBuilder response = new StringBuilder();

                while ((inputLine = in.readLine()) != null) {
                    response.append(inputLine);
                }
                in.close();

                System.out.println(response.toString());
            } else {
                System.out.println("POST request failed. Response Code: " + responseCode);
            }

            fileInputStream.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

```

```javascript
const url = 'http://localhost/api_v2/library/123e4567-e89b-12d3-a456-426614174000/file';
const fileInput = document.querySelector('input[type="file"]'); // Assuming you have an input for file selection

const formData = new FormData();
formData.append('file', fileInput.files[0]); // Add the selected file

fetch(url, {
  method: 'POST',
  headers: {
    'Accept': 'application/json'
  },
  body: formData
})
  .then(response => {
    if (!response.ok) {
      throw new Error('Network response was not ok ' + response.statusText);
    }
    return response.json();
  })
  .then(data => console.log(data))
  .catch(error => console.error('There was a problem with the fetch operation:', error));

```

```shell
curl -X 'POST' \
  'http://localhost/api_v2/library/123e4567-e89b-12d3-a456-426614174000/file' \
  -H 'accept: application/json' \
  -H 'Content-Type: multipart/form-data' \
  -F 'file=@openapi.yaml'
```

> The above request, on success, returns JSON structured like this:

```json
{
  "name": "string",
  "document_type": "string",
  "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "library_id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "document_url": "string",
  "s3_key": "string",
  "doc_metadata": "string",
  "document": {
    "id": "string",
    "file_name": "string",
    "file_path": "string",
    "save_name": "string",
    "s3_path": "string",
    "status": "string",
    "md5_hash": "string",
    "parsed": true,
    "page_count": 0,
    "para_count": 0,
    "word_count": 0,
    "char_count": 0,
    "file_size": "string",
    "doc_processed_version": "string"
  }
}
```

**Description:** Create Document

### HTTP Request 
***POST*** request on `/api_v2/library/{library_id}/file` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| library_id | path |  | Yes |  |

**Responses**

| Code | Description |
| ---- | ----------- |
| 201 | Successful Response |
| 422 | Validation Error |

## Delete Document

> Example Usage: 

```python
import requests

url = 'http://localhost/api_v2/document/7650e878-ec84-44f0-b7b9-c068f67bb41b/delete'
headers = {
    'accept': 'application/json',
    'Authorization': 'Bearer <auth-token>'
}

response = requests.delete(url, headers=headers)
print(response.status_code)
print(response.text)  # If needed, print the response body

```

```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;

public class Main {
    public static void main(String[] args) {
        String url = "http://localhost/api_v2/document/7650e878-ec84-44f0-b7b9-c068f67bb41b/delete";

        try {
            HttpURLConnection con = (HttpURLConnection) new URL(url).openConnection();
            con.setRequestMethod("DELETE");
            con.setRequestProperty("Accept", "application/json");
            con.setRequestProperty("Authorization", "Bearer <auth-token>");

            int responseCode = con.getResponseCode();
            System.out.println("Response Code: " + responseCode);

            BufferedReader in = new BufferedReader(new InputStreamReader(con.getInputStream()));
            String inputLine;
            StringBuilder content = new StringBuilder();

            while ((inputLine = in.readLine()) != null) {
                content.append(inputLine);
            }

            // Close connections
            in.close();
            con.disconnect();

            // Print result
            System.out.println(content.toString());

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

```

```javascript
const url = 'http://localhost/api_v2/document/7650e878-ec84-44f0-b7b9-c068f67bb41b/delete';

const headers = {
  'Accept': 'application/json',
  'Authorization': 'Bearer <auth-token>'
};

fetch(url, {
  method: 'DELETE',
  headers: headers
})
  .then(response => {
    console.log('Response Code:', response.status);
    return response.text();  // If you need to print the response body
  })
  .then(data => console.log(data))
  .catch(error => console.error('Error:', error));

```

```shell
curl -X 'DELETE' \
  'http://localhost/api_v2/document/7650e878-ec84-44f0-b7b9-c068f67bb41b/delete' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer <auth-token>'

```

**Description:** Delete Document

### HTTP Request 
***DELETE*** request on `/api_v2/document/{doc_id}/delete` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| doc_id | path |  | Yes |  |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 422 | Validation Error |

## Update Document

> Example Usage: 

```python
import requests

url = 'http://localhost/api_v2/document/7650e878-ec84-44f0-b7b9-c068f67bb41b/update?name=name'
headers = {
    'accept': 'application/json',
    'Authorization': 'Bearer <auth-token>'
}

response = requests.post(url, headers=headers)
print(response.status_code)
print(response.text)  # If needed, print the response body
```

```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;

public class Main {
    public static void main(String[] args) {
        String url = "http://localhost/api_v2/document/7650e878-ec84-44f0-b7b9-c068f67bb41b/update?name=name";

        try {
            HttpURLConnection con = (HttpURLConnection) new URL(url).openConnection();
            con.setRequestMethod("POST");
            con.setRequestProperty("Accept", "application/json");
            con.setRequestProperty("Authorization", "Bearer <auth-token>");

            int responseCode = con.getResponseCode();
            System.out.println("Response Code: " + responseCode);

            BufferedReader in = new BufferedReader(new InputStreamReader(con.getInputStream()));
            String inputLine;
            StringBuilder content = new StringBuilder();

            while ((inputLine = in.readLine()) != null) {
                content.append(inputLine);
            }

            // Close connections
            in.close();
            con.disconnect();

            // Print result
            System.out.println(content.toString());

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

```

```javascript
const url = 'http://localhost/api_v2/document/7650e878-ec84-44f0-b7b9-c068f67bb41b/update?name=name';

const headers = {
  'Accept': 'application/json',
  'Authorization': 'Bearer <auth-token>'
};

fetch(url, {
  method: 'POST',
  headers: headers
})
  .then(response => {
    console.log('Response Code:', response.status);
    return response.text();  // If you need to print the response body
  })
  .then(data => console.log(data))
  .catch(error => console.error('Error:', error));

```

```shell
curl -X 'POST' \
  'http://localhost/api_v2/document/7650e878-ec84-44f0-b7b9-c068f67bb41b/update?name=name' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer <auth-token>' \
  -d ''

```

**Description:** Update Document

### HTTP Request 
***POST*** request on `/api_v2/document/{doc_id}/update` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| doc_id | path |  | Yes |  |
| name | query |  | Yes |  |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 422 | Validation Error |

## Get Document By Page

> Example Usage: 

```python
import requests

url = 'http://localhost/api_v2/document/7650e878-ec84-44f0-b7b9-c068f67bb41b/page?page=3&answer_id=7650e878-ec84-44f0-b7b9-c068f67bb41b'
headers = {
    'accept': '*/*',
    'Authorization': 'Bearer <auth-token>'
}

response = requests.get(url, headers=headers)
print(response.status_code)
print(response.text)  # If needed, print the response body

```

```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;

public class Main {
    public static void main(String[] args) {
        String url = "http://localhost/api_v2/document/7650e878-ec84-44f0-b7b9-c068f67bb41b/page?page=3&answer_id=7650e878-ec84-44f0-b7b9-c068f67bb41b";

        try {
            HttpURLConnection con = (HttpURLConnection) new URL(url).openConnection();
            con.setRequestMethod("GET");
            con.setRequestProperty("Accept", "*/*");
            con.setRequestProperty("Authorization", "Bearer <auth-token>");

            int responseCode = con.getResponseCode();
            System.out.println("Response Code: " + responseCode);

            BufferedReader in = new BufferedReader(new InputStreamReader(con.getInputStream()));
            String inputLine;
            StringBuilder content = new StringBuilder();

            while ((inputLine = in.readLine()) != null) {
                content.append(inputLine);
            }

            // Close connections
            in.close();
            con.disconnect();

            // Print result
            System.out.println(content.toString());

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

```

```javascript
const url = 'http://localhost/api_v2/document/7650e878-ec84-44f0-b7b9-c068f67bb41b/page?page=3&answer_id=7650e878-ec84-44f0-b7b9-c068f67bb41b';

const headers = {
  'Accept': '*/*',
  'Authorization': 'Bearer <auth-token>'
};

fetch(url, {
  method: 'GET',
  headers: headers
})
  .then(response => {
    console.log('Response Code:', response.status);
    return response.text();  // If you need to print the response body
  })
  .then(data => console.log(data))
  .catch(error => console.error('Error:', error));

```

```shell
curl -X 'GET' \
  'http://localhost/api_v2/document/7650e878-ec84-44f0-b7b9-c068f67bb41b/page?page=3&answer_id=7650e878-ec84-44f0-b7b9-c068f67bb41b' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer <auth-token>'

```

**Description:** Get Document

### HTTP Request 
***GET*** request on `/api_v2/document/{doc_id}/page` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| doc_id | path |  | Yes |  |
| page | query |  | No |  |
| answer_id | query |  | No |  |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 422 | Validation Error |



# Transaction API 

## Create New Transaction


> Example Usage: 

```python
import requests
import json

url = 'http://localhost/api_v2/library/123e4567-e89b-12d3-a456-426614174000/transaction'
headers = {
    'accept': 'application/json',
    'Content-Type': 'application/json'
}
data = {
    "query_string": "string",
    "transaction_ids": [],
    "agent_persona": "Your name is Subtl Bot. You are an AI assistant designed by researchers and engineers of Subtl.ai to help users based on private knowledge."
}

response = requests.post(url, headers=headers, data=json.dumps(data))
print(response.json())

```

```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.io.OutputStream;
import java.net.HttpURLConnection;
import java.net.URL;

public class Main {
    public static void main(String[] args) {
        String url = "http://localhost/api_v2/library/123e4567-e89b-12d3-a456-426614174000/transaction";
        String jsonInputString = "{\"query_string\": \"string\", \"transaction_ids\": [], \"agent_persona\": \"Your name is Subtl Bot. You are an AI assistant designed by researchers and engineers of Subtl.ai to help users based on private knowledge.\"}";

        try {
            HttpURLConnection con = (HttpURLConnection) new URL(url).openConnection();
            con.setRequestMethod("POST");
            con.setRequestProperty("Accept", "application/json");
            con.setRequestProperty("Content-Type", "application/json");
            con.setDoOutput(true);

            try (OutputStream os = con.getOutputStream()) {
                byte[] input = jsonInputString.getBytes("utf-8");
                os.write(input, 0, input.length);
            }

            int responseCode = con.getResponseCode();
            System.out.println("Response Code: " + responseCode);

            if (responseCode == HttpURLConnection.HTTP_OK) {
                BufferedReader in = new BufferedReader(new InputStreamReader(con.getInputStream()));
                StringBuilder response = new StringBuilder();
                String inputLine;

                while ((inputLine = in.readLine()) != null) {
                    response.append(inputLine);
                }
                in.close();

                System.out.println(response.toString());
            } else {
                System.out.println("POST request failed. Response Code: " + responseCode);
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

```

```javascript
const url = 'http://localhost/api_v2/library/123e4567-e89b-12d3-a456-426614174000/transaction';
const data = {
  query_string: "string",
  transaction_ids: [],
  agent_persona: "Your name is Subtl Bot. You are an AI assistant designed by researchers and engineers of Subtl.ai to help users based on private knowledge."
};

fetch(url, {
  method: 'POST',
  headers: {
    'Accept': 'application/json',
    'Content-Type': 'application/json'
  },
  body: JSON.stringify(data)
})
  .then(response => {
    if (!response.ok) {
      throw new Error('Network response was not ok ' + response.statusText);
    }
    return response.json();
  })
  .then(data => console.log(data))
  .catch(error => console.error('There was a problem with the fetch operation:', error));

```

```shell
curl -X 'POST' \
  'http://localhost/api_v2/library/123e4567-e89b-12d3-a456-426614174000/transaction' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "query_string": "string",
  "transaction_ids": [],
  "agent_persona": "Your name is Subtl Bot. You are an AI assistant designed by researchers and engineers of Subtl.ai to help users based on private knowledge."
}'
```

> The above request, on success, returns JSON structured like this:

```json
{
  "query_string": "string",
  "user_id": "string",
  "response_type": "string",
  "time_taken": "string",
  "augmented_query": "string",
  "generated_answer": "",
  "answers": [
    {
      "transaction_id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "page_no": 0,
      "answer": "string",
      "highlights": "string",
      "long_answer": "",
      "phrase_start_pos": -1,
      "phrase_end_pos": -1,
      "phrase_start_pos_long": -1,
      "phrase_end_pos_long": -1,
      "doc_metadata": "",
      "score": 0,
      "document_clicked": false,
      "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "document": {
        "name": "string",
        "document_type": "",
        "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
        "upload_date": "2024-10-07T22:28:25.123Z",
        "document_url": "string",
        "s3_key": "string",
        "document_id": "string",
        "library_id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
        "account_id": "string",
        "doc_metadata": ""
      }
    }
  ],
  "timestamp": "2024-10-07T22:28:25.123Z",
  "resolution_status": true,
  "feedback": "string",
  "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
}
```

**Description:** Create New Transaction

### HTTP Request 
***POST*** request for `/api_v2/library/{library_id}/transaction` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| library_id | path |  | Yes |  |

**Responses**


| Code | Description |
| ---- | ----------- |
| 201 | Successful Response |
| 422 | Validation Error |

