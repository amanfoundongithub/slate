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

## Setting Up Docker Container

Create two docker containers:

- Create an external network for both stacks


`>>> docker network create traefik-public`

- Create an external minio volume for the stacks


`>>> docker volume create subtl_bot_minio-data`


## Running the Doc Parser stack

Go to the doc parser directory:


`>>> cd subtl_doc_parser`

Create an `.env` file by copying the variables from `.env.example`:


`>>> cp .env.example .env`


Adjust the `.env` variables appropriately. 


Now spin up the stack using the following command:

`>>> ./subtl_doc_parser.sh -g -d -- up --build -d`

This will build and run the `subtl_doc_parser` stack.


## Running the Web API stack 

Create an `.env` file by copying the variables from `.env.example`:


`>>> cp .env.example .env`


Adjust the `.env` variables appropriately. 


Copy `subtl_llm/app/backends/config.json.example` to `subtl_llm/app/backends/config.json` and add backend configurations in the file:

`>>> cp subtl_llm/app/backends/config.json.example subtl_llm/app/backends/config.json`

Now spin up the stack using the following command:

`>>> ./run.sh -d -- up --build -d`

This will build and run the `subtl_bot` stack.

The APIs will now go live at `localhost`. 


## Request an Authentication Token

Some of the APIs, like the `Document` APIs requires an authentication token to validate a request. To do this, you have to request an API token from the us to get started with these APIs.

# Account API 


<!--- Account READ BY ID --->
## Reading An Account By ID

**Description:** This method allows you to fetch details of an account by the ID of the account. 

### HTTP Request 
`***GET*** /api_v2/account/{account_id}` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| account_id | path | The ID of the account | Yes | String |

```python
import requests

url = "http://localhost/api_v2/account/account_id"
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
            String url = "http://localhost/api_v2/account/account_id";
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
const url = 'http://localhost/api_v2/account/account_id';

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
  'http://localhost/api_v2/account/account_id' \
  -H 'accept: application/json'
```

> The above request, on a successful request, returns JSON structured like this:

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

**Responses**

| Code | Description | 
| ---- | ----------- |
| 200 | Successful Response |
| 422 | Validation Error |

## Reading An Account By Email 

**Description:** This method allows you to fetch details of an account by the email of the account. 

### HTTP Request 
`***GET*** /api_v2/account/account_by_email` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| email_id | query | The email we want to find | Yes |  Email String |

```python
import requests

url = "http://localhost/api_v2/account/account_by_email"
params = {"email_id": "email_id"}
headers = {
    "accept": "application/json"
}

response = requests.get(url, headers=headers, params=params)
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
            String url = "http://localhost/api_v2/account/account_by_email?email_id=email_id";
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
const url = 'http://localhost/api_v2/account/account_by_email?email_id=email_id';

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
  'http://localhost/api_v2/account/account_by_email?email_id=email_id' \
  -H 'accept: application/json'
```

> The above request, on a successful request, returns JSON structured like this:

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

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 422 | Validation Error |


## Deleting An Account By ID

**Summary:** Delete Account

**Description:** Delete a account.

### HTTP Request 
`***DELETE*** /api_v2/account/{account_id}` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| account_id | path | The account ID to be deleted | Yes | String |

```python
import requests

url = "http://localhost/api_v2/account/123456790"
headers = {
    "accept": "application/json"
}

response = requests.delete(url, headers=headers)
print(response.status_code)

```

```java
import java.net.HttpURLConnection;
import java.net.URL;

public class Main {
    public static void main(String[] args) {
        try {
            String url = "http://localhost/api_v2/account/123456790";
            URL obj = new URL(url);
            HttpURLConnection con = (HttpURLConnection) obj.openConnection();
            
            // Set request method to DELETE
            con.setRequestMethod("DELETE");
            con.setRequestProperty("Accept", "application/json");

            // Get the response code
            int responseCode = con.getResponseCode();
            System.out.println("Response Code: " + responseCode);

            if (responseCode == HttpURLConnection.HTTP_OK) {
                System.out.println("Account successfully deleted.");
            } else {
                System.out.println("Failed to delete the account.");
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

```

```javascript
const url = 'http://localhost/api_v2/account/123456790';

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
    console.log('Account successfully deleted');
  })
  .catch(error => console.error('There was a problem with the DELETE operation:', error));

```

```shell
curl -X 'DELETE' \
  'http://localhost/api_v2/account/123456790' \
  -H 'accept: application/json'
```

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 422 | Validation Error |


> The above request, on a successful request, returns JSON structured like this:

```json
{
  "message": "string"
}
```


## Reading Current Account

**Description:** This API allows you to get te details of the current account.

### HTTP Request 
`***GET*** /api_v2/account/me` 

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |


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

> The above request, on a successful request, returns JSON structured like this:

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

## Updating Current Account

**Summary:** Update Account Me

**Description:** Update own account.

### HTTP Request 
`***PATCH*** /api_v2/account/me` 

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

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 422 | Validation Error |


> The above request, on a successful request, returns JSON structured like this:

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

## Reading All Accounts

**Description:** This API allows you to get details of all the accounts that are stored in the database. 

### HTTP Request 
`***GET*** /api_v2/account/` 

```python
import requests

url = "http://localhost/api_v2/account/"
params = {
    "top_doc_counts": "false",
    "top_transaction_count": "false",
    "skip": 0,
    "limit": 100
}
headers = {
    "accept": "application/json"
}

response = requests.get(url, headers=headers, params=params)
print(response.json())

```

```shell
curl -X 'GET' \
  'http://localhost/api_v2/account/?top_doc_counts=false&top_transaction_count=false&skip=0&limit=100' \
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
            String url = "http://localhost/api_v2/account/?top_doc_counts=false&top_transaction_count=false&skip=0&limit=100";
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
const url = 'http://localhost/api_v2/account/?top_doc_counts=false&top_transaction_count=false&skip=0&limit=100';

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

> The above request, on a successful request, returns JSON structured like this:

```json
{
  "data": [
    {
      "email": "string",
      "email_verified": false,
      "given_name": "string",
      "family_name": "string",
      "picture": "string",
      "id": "string",
      "doc_count": 0,
      "transaction_count": 0
    }
  ],
  "count": 0
}
```

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| top_doc_counts | query |  | No |  |
| top_transaction_count | query |  | No |  |
| skip | query |  | No |  |
| limit | query |  | No |  |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 422 | Validation Error |



# Workspace API
## Get My Workspaces

**Summary:** Fetches the current workspace 

### HTTP Request 
`***GET*** /api_v2/workspace/` 

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |

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

> The above request, on a successful request, returns JSON structured like this:

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

## Creates a Workspace

**Summary:** Create Workspace

### HTTP Request 
`***POST*** /api_v2/workspace/` 

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

> The above request, on a successful request, returns JSON structured like this:

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

**Responses**

| Code | Description |
| ---- | ----------- |
| 201 | Successful Response |
| 422 | Validation Error |


## Get My Workspaces

**Summary:** Get My Workspaces

### HTTP Request 
`***GET*** /api_v2/workspace/get_user_worspace` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| populate_libraries | query |  | No |  |
| account_id | query |  | No |  |

```python
import requests

url = "http://localhost/api_v2/workspace/get_user_worspace"
params = {
    "populate_libraries": "true",
    "account_id": "account_id"
}
headers = {
    "accept": "application/json"
}

response = requests.get(url, headers=headers, params=params)
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
            String url = "http://localhost/api_v2/workspace/get_user_worspace?populate_libraries=true&account_id=account_id";
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
const url = 'http://localhost/api_v2/workspace/get_user_worspace?populate_libraries=true&account_id=account_id';

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
  'http://localhost/api_v2/workspace/get_user_worspace?populate_libraries=true&account_id=account_id' \
  -H 'accept: application/json'
```

> The above request, on a successful request, returns JSON structured like this:

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

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 422 | Validation Error |

## Get My Workspaces With Libraries

**Summary:** Get My Workspaces With Libraries

### HTTP Request 
`***GET*** /api_v2/workspace/all` 

```python
import requests

url = "http://localhost/api_v2/workspace/all"
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
            String url = "http://localhost/api_v2/workspace/all";
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
const url = 'http://localhost/api_v2/workspace/all';

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
  'http://localhost/api_v2/workspace/all' \
  -H 'accept: application/json'
```

> The above request, on a successful request, returns JSON structured like this:

```json
[
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
      "start_date": "2024-10-07T22:13:15.735Z",
      "end_date": "2024-10-07T22:13:15.735Z",
      "active": true
    }
  }
]
```

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |

## Update Workspace

**Summary:** Update Workspace

### HTTP Request 
`***PATCH*** /api_v2/workspace/{workspace_id}` 

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

> The above request, on a successful request, returns JSON structured like this:

```json
{
  "name": "string",
  "max_threshold": 0,
  "is_public": true,
  "is_default": true,
  "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
}
```

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

**Summary:** Delete Workspace

### HTTP Request 
`***DELETE*** /api_v2/workspace/{workspace_id}` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| workspace_id | path |  | Yes |  |

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

> The above request, on a successful request, returns JSON structured like this:

```json
"string"
```

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 422 | Validation Error |

## Get Workspace Users

**Summary:** Get Workspace Users

### HTTP Request 
`***GET*** /api_v2/workspace/{workspace_id}/users` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| workspace_id | path |  | Yes |  |

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

> The above request, on a successful request, returns JSON structured like this:

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

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 422 | Validation Error |

## Add User

**Summary:** Add User

### HTTP Request 
`***POST*** /api_v2/workspace/{workspace_id}/add_user` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| workspace_id | path |  | Yes |  |
| user_id | query |  | Yes |  |
| is_admin | query |  | No |  |

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

> The above request, on a successful request, returns JSON structured like this:

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

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 422 | Validation Error |

## Create New Library

**Summary:** Create New Library

### HTTP Request 
`***POST*** /api_v2/workspace/{workspace_id}/add_library` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| workspace_id | path |  | Yes |  |

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

> The above request, on a successful request, returns JSON structured like this:

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

**Responses**

| Code | Description |
| ---- | ----------- |
| 201 | Successful Response |
| 422 | Validation Error |

## Port New Library

**Summary:** Port New Library

### HTTP Request 
`***POST*** /api_v2/workspace/{workspace_id}/port_library` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| workspace_id | path |  | Yes |  |
| group_idx | query |  | Yes |  |

```python
import requests

url = 'http://localhost/api_v2/workspace/123e4567-e89b-12d3-a456-426614174000/port_library?group_idx={group_idx}'
headers = {
    'accept': 'application/json'
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
            String url = "http://localhost/api_v2/workspace/123e4567-e89b-12d3-a456-426614174000/port_library?group_idx={group_idx}";
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
const url = 'http://localhost/api_v2/workspace/123e4567-e89b-12d3-a456-426614174000/port_library?group_idx={group_idx}';

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
  'http://localhost/api_v2/workspace/123e4567-e89b-12d3-a456-426614174000/port_library?group_idx=%7Bgroup_idx%7D' \
  -H 'accept: application/json' \
  -d ''
```

> The above request, on a successful request, returns JSON structured like this:

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

**Responses**

| Code | Description |
| ---- | ----------- |
| 201 | Successful Response |
| 422 | Validation Error |

## Get Workspace Libraries

**Summary:** Get Workspace Libraries

### HTTP Request 
`***GET*** /api_v2/workspace/{workspace_id}/libraries` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| workspace_id | path |  | Yes |  |

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

> The above request, on a successful request, returns JSON structured like this:

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

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 422 | Validation Error |

## Get Workspace Public Libraries

**Summary:** Get Workspace Public Libraries

### HTTP Request 
`***GET*** /api_v2/workspace/{workspace_id}/public_libraries` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| workspace_id | path |  | Yes |  |

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

> The above request, on a successful request, returns JSON structured like this:

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

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 422 | Validation Error |



## Send Workspace Invite

**Summary:** Send Workspace Invite

### HTTP Request 
`***POST*** /api_v2/workspace/{workspace_id}/send_invite` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| workspace_id | path |  | Yes |  |

```python
import requests
import json

url = 'http://localhost/api_v2/workspace/123e4567-e89b-12d3-a456-426614174000/send_invite'
headers = {
    'accept': 'application/json',
    'Content-Type': 'application/json'
}
data = {
    "user_identifier": "string",
    "is_admin_request": False
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
            String url = "http://localhost/api_v2/workspace/123e4567-e89b-12d3-a456-426614174000/send_invite";
            URL obj = new URL(url);
            HttpURLConnection con = (HttpURLConnection) obj.openConnection();
            
            con.setRequestMethod("POST");
            con.setRequestProperty("Accept", "application/json");
            con.setRequestProperty("Content-Type", "application/json");
            con.setDoOutput(true);
            
            String jsonInputString = "{\"user_identifier\": \"string\", \"is_admin_request\": false}";

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
const url = 'http://localhost/api_v2/workspace/123e4567-e89b-12d3-a456-426614174000/send_invite';

const data = {
  user_identifier: "string",
  is_admin_request: false
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
  'http://localhost/api_v2/workspace/123e4567-e89b-12d3-a456-426614174000/send_invite' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "user_identifier": "string",
  "is_admin_request": false
}'
```

> The above request, on a successful request, returns JSON structured like this:

```json
{}
```

**Responses**

| Code | Description |
| ---- | ----------- |
| 201 | Successful Response |
| 422 | Validation Error |

## Accept Workspace Invite

**Summary:** Accept Workspace Invite

### HTTP Request 
`***POST*** /api_v2/workspace/{invitation_id}/accept_invite` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| invitation_id | path |  | Yes |  |

```python
import requests

url = 'http://localhost/api_v2/workspace/123e4567-e89b-12d3-a456-426614174000/accept_invite'
headers = {
    'accept': 'application/json'
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
            String url = "http://localhost/api_v2/workspace/123e4567-e89b-12d3-a456-426614174000/accept_invite";
            URL obj = new URL(url);
            HttpURLConnection con = (HttpURLConnection) obj.openConnection();
            
            con.setRequestMethod("POST");
            con.setRequestProperty("Accept", "application/json");
            con.setDoOutput(true); // Enable output if you want to send a body

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
const url = 'http://localhost/api_v2/workspace/123e4567-e89b-12d3-a456-426614174000/accept_invite';

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
  'http://localhost/api_v2/workspace/123e4567-e89b-12d3-a456-426614174000/accept_invite' \
  -H 'accept: application/json' \
  -d ''
```

> The above request, on a successful request, returns JSON structured like this:

```json
{}
```

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 422 | Validation Error |

##  Request To Join Workspace

**Summary:** Request To Join Workspace

### HTTP Request 
`***POST*** /api_v2/workspace/{workspace_id}/ask_to_join` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| workspace_id | path |  | Yes |  |

```python
import requests

url = 'http://localhost/api_v2/workspace/123e4567-e89b-12d3-a456-426614174000/ask_to_join'
headers = {
    'accept': 'application/json'
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
            String url = "http://localhost/api_v2/workspace/123e4567-e89b-12d3-a456-426614174000/ask_to_join";
            URL obj = new URL(url);
            HttpURLConnection con = (HttpURLConnection) obj.openConnection();
            
            con.setRequestMethod("POST");
            con.setRequestProperty("Accept", "application/json");
            con.setDoOutput(true); // Enable output if you want to send a body

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
const url = 'http://localhost/api_v2/workspace/123e4567-e89b-12d3-a456-426614174000/ask_to_join';

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
  'http://localhost/api_v2/workspace/123e4567-e89b-12d3-a456-426614174000/ask_to_join' \
  -H 'accept: application/json' \
  -d ''
```
> The above request, on a successful request, returns JSON structured like this:

```json
{}
```

**Responses**

| Code | Description |
| ---- | ----------- |
| 201 | Successful Response |
| 422 | Validation Error |

## Accept Workspace Join Request

**Summary:** Accept Workspace Join Request

### HTTP Request 
`***POST*** /api_v2/workspace/{invitation_id}/accept_request` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| invitation_id | path |  | Yes |  |

```python
import requests

url = 'http://localhost/api_v2/workspace/123e4567-e89b-12d3-a456-426614174000/accept_request'
headers = {
    'accept': 'application/json'
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
            String url = "http://localhost/api_v2/workspace/123e4567-e89b-12d3-a456-426614174000/accept_request";
            URL obj = new URL(url);
            HttpURLConnection con = (HttpURLConnection) obj.openConnection();
            
            con.setRequestMethod("POST");
            con.setRequestProperty("Accept", "application/json");
            con.setDoOutput(true); // Enable output if you want to send a body

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
const url = 'http://localhost/api_v2/workspace/123e4567-e89b-12d3-a456-426614174000/accept_request';

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
  'http://localhost/api_v2/workspace/123e4567-e89b-12d3-a456-426614174000/accept_request' \
  -H 'accept: application/json' \
  -d ''
```

> The above request, on a successful request, returns JSON structured like this:

```json
{}
```

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 422 | Validation Error |

## Reject Invitation

**Summary:** Reject Invitation

### HTTP Request 
`***POST*** /api_v2/workspace/{invitation_id}/reject_invite` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| invitation_id | path |  | Yes |  |

```python
import requests

url = 'http://localhost/api_v2/workspace/123e4567-e89b-12d3-a456-426614174000/reject_invite'
headers = {
    'accept': 'application/json'
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
            String url = "http://localhost/api_v2/workspace/123e4567-e89b-12d3-a456-426614174000/reject_invite";
            URL obj = new URL(url);
            HttpURLConnection con = (HttpURLConnection) obj.openConnection();
            
            con.setRequestMethod("POST");
            con.setRequestProperty("Accept", "application/json");
            con.setDoOutput(true); // Enable output if you want to send a body

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
const url = 'http://localhost/api_v2/workspace/123e4567-e89b-12d3-a456-426614174000/reject_invite';

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
  'http://localhost/api_v2/workspace/123e4567-e89b-12d3-a456-426614174000/reject_invite' \
  -H 'accept: application/json' \
  -d ''
```

> The above request, on a successful request, returns JSON structured like this:

```json
{}
```

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 422 | Validation Error |

## Edit User

**Summary:** Edit User

### HTTP Request 
`***POST*** /api_v2/workspace/{workspace_id}/edit_user` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| workspace_id | path |  | Yes |  |

```python
import requests
import json

url = 'http://localhost/api_v2/workspace/123e4567-e89b-12d3-a456-426614174000/edit_user'
headers = {
    'accept': 'application/json',
    'Content-Type': 'application/json'
}
data = {
    "user_id": "string",
    "is_admin": True
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
            String url = "http://localhost/api_v2/workspace/123e4567-e89b-12d3-a456-426614174000/edit_user";
            URL obj = new URL(url);
            HttpURLConnection con = (HttpURLConnection) obj.openConnection();
            
            con.setRequestMethod("POST");
            con.setRequestProperty("Accept", "application/json");
            con.setRequestProperty("Content-Type", "application/json");
            con.setDoOutput(true); // Enable output to send a body

            String jsonInputString = "{\"user_id\": \"string\", \"is_admin\": true}";

            try(OutputStream os = con.getOutputStream()) {
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
const url = 'http://localhost/api_v2/workspace/123e4567-e89b-12d3-a456-426614174000/edit_user';

const data = {
  user_id: "string",
  is_admin: true
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
  'http://localhost/api_v2/workspace/123e4567-e89b-12d3-a456-426614174000/edit_user' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "user_id": "string",
  "is_admin": true
}'
```

> The above request, on a successful request, returns JSON structured like this:

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

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 422 | Validation Error |

## Remove User

**Summary:** Remove User

### HTTP Request 
`***POST*** /api_v2/workspace/{workspace_id}/remove_user` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| workspace_id | path |  | Yes |  |

```python
import requests
import json

url = 'http://localhost/api_v2/workspace/123e4567-e89b-12d3-a456-426614174000/remove_user'
headers = {
    'accept': 'application/json',
    'Content-Type': 'application/json'
}
data = {
    "user_id": "string"
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
            String url = "http://localhost/api_v2/workspace/123e4567-e89b-12d3-a456-426614174000/remove_user";
            URL obj = new URL(url);
            HttpURLConnection con = (HttpURLConnection) obj.openConnection();
            
            con.setRequestMethod("POST");
            con.setRequestProperty("Accept", "application/json");
            con.setRequestProperty("Content-Type", "application/json");
            con.setDoOutput(true); // Enable output to send a body

            String jsonInputString = "{\"user_id\": \"string\"}";

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
const url = 'http://localhost/api_v2/workspace/123e4567-e89b-12d3-a456-426614174000/remove_user';

const data = {
  user_id: "string"
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
  'http://localhost/api_v2/workspace/123e4567-e89b-12d3-a456-426614174000/remove_user' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "user_id": "string"
}'
```

> The above request, on a successful request, returns JSON structured like this:

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

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 422 | Validation Error |

# Library API
## Read Library Relation

**Summary:** Read Library Relation

### HTTP Request 
`***GET*** /api_v2/library/{library_id}` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| library_id | path |  | Yes |  |

```python
import requests

url = 'http://localhost/api_v2/library/123e4567-e89b-12d3-a456-426614174000'
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
            String url = "http://localhost/api_v2/library/123e4567-e89b-12d3-a456-426614174000";
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
const url = 'http://localhost/api_v2/library/123e4567-e89b-12d3-a456-426614174000';

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
  'http://localhost/api_v2/library/123e4567-e89b-12d3-a456-426614174000' \
  -H 'accept: application/json'
```

> The above request, on a successful request, returns JSON structured like this:

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


**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 422 | Validation Error |

## Update Library Details

**Summary:** Update Library Details

### HTTP Request 
`***PATCH*** /api_v2/library/{library_id}` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| library_id | path |  | Yes |  |

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

> The above request, on a successful request, returns JSON structured like this:

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

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 422 | Validation Error |

## Delete Library By Id 

**Summary:** Delete Library By Id

### HTTP Request 
`***DELETE*** /api_v2/library/{library_id}` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| library_id | path |  | Yes |  |
| ignore_backend | query |  | No |  |

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

> The above request, on a successful request, returns JSON structured like this:

```json
"string"
```

**Responses**

| Code | Description |
| ---- | ----------- |
| 204 | Successful Response |
| 422 | Validation Error |

## Add User To Library 

**Summary:** Add User To Library 

### HTTP Request 
`***POST*** /api_v2/library/{library_id}/add_user` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| library_id | path |  | Yes |  |

```python
import requests
import json

url = 'http://localhost/api_v2/library/123e4567-e89b-12d3-a456-426614174000/add_user'
headers = {
    'accept': 'application/json',
    'Content-Type': 'application/json'
}
data = {
    "is_admin": False,
    "can_upload": True,
    "email": "string"
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
            String url = "http://localhost/api_v2/library/123e4567-e89b-12d3-a456-426614174000/add_user";
            URL obj = new URL(url);
            HttpURLConnection con = (HttpURLConnection) obj.openConnection();
            
            con.setRequestMethod("POST");
            con.setRequestProperty("Accept", "application/json");
            con.setRequestProperty("Content-Type", "application/json");
            con.setDoOutput(true); // Enable output to send a body

            String jsonInputString = "{\"is_admin\": false, \"can_upload\": true, \"email\": \"string\"}";

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
const url = 'http://localhost/api_v2/library/123e4567-e89b-12d3-a456-426614174000/add_user';

const data = {
  is_admin: false,
  can_upload: true,
  email: "string"
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
  'http://localhost/api_v2/library/123e4567-e89b-12d3-a456-426614174000/add_user' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "is_admin": false,
  "can_upload": true,
  "email": "string"
}'
```

> The above request, on a successful request, returns JSON structured like this:

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

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 422 | Validation Error |

## Get Library Users

**Summary:** Get Library Users

### HTTP Request 
`***GET*** /api_v2/library/{library_id}/users` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| library_id | path |  | Yes |  |

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

> The above request, on a successful request, returns JSON structured like this:

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

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 422 | Validation Error |

## Join Public Library

**Summary:** Join Public Library

### HTTP Request 
`***POST*** /api_v2/library/{library_id}/join` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| library_id | path |  | Yes |  |

```python
import requests

url = 'http://localhost/api_v2/library/123e4567-e89b-12d3-a456-426614174000/join'
headers = {
    'accept': 'application/json'
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
            String url = "http://localhost/api_v2/library/123e4567-e89b-12d3-a456-426614174000/join";
            URL obj = new URL(url);
            HttpURLConnection con = (HttpURLConnection) obj.openConnection();
            
            con.setRequestMethod("POST");
            con.setRequestProperty("Accept", "application/json");
            con.setDoOutput(true); // Enable output to send a body

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
const url = 'http://localhost/api_v2/library/123e4567-e89b-12d3-a456-426614174000/join';

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
  'http://localhost/api_v2/library/123e4567-e89b-12d3-a456-426614174000/join' \
  -H 'accept: application/json' \
  -d ''
```

> The above request, on a successful request, returns JSON structured like this:

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

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 422 | Validation Error |

## Remove User

**Summary:** Remove User

### HTTP Request 
`***POST*** /api_v2/library/{library_id}/remove_user` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| library_id | path |  | Yes |  |

```python
import requests
import json

url = 'http://localhost/api_v2/library/123e4567-e89b-12d3-a456-426614174000/remove_user'
headers = {
    'accept': 'application/json',
    'Content-Type': 'application/json'
}
data = {
    "user_id": "string"
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
            String url = "http://localhost/api_v2/library/123e4567-e89b-12d3-a456-426614174000/remove_user";
            URL obj = new URL(url);
            HttpURLConnection con = (HttpURLConnection) obj.openConnection();
            
            con.setRequestMethod("POST");
            con.setRequestProperty("Accept", "application/json");
            con.setRequestProperty("Content-Type", "application/json");
            con.setDoOutput(true); // Enable output to send a body

            String jsonInputString = "{\"user_id\": \"string\"}";

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
const url = 'http://localhost/api_v2/library/123e4567-e89b-12d3-a456-426614174000/remove_user';

const data = {
  user_id: "string"
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
  'http://localhost/api_v2/library/123e4567-e89b-12d3-a456-426614174000/remove_user' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "user_id": "string"
}'
```

> The above request, on a successful request, returns JSON structured like this:

```json
"string
```

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 422 | Validation Error |

## Edit User

**Summary:** Edit User

### HTTP Request 
`***POST*** /api_v2/library/{library_id}/edit_user` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| library_id | path |  | Yes |  |

```python
import requests
import json

url = 'http://localhost/api_v2/library/123e4567-e89b-12d3-a456-426614174000/edit_user'
headers = {
    'accept': 'application/json',
    'Content-Type': 'application/json'
}
data = {
    "user_id": "string",
    "is_admin": True,
    "can_upload": True
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
            String url = "http://localhost/api_v2/library/123e4567-e89b-12d3-a456-426614174000/edit_user";
            URL obj = new URL(url);
            HttpURLConnection con = (HttpURLConnection) obj.openConnection();
            
            con.setRequestMethod("POST");
            con.setRequestProperty("Accept", "application/json");
            con.setRequestProperty("Content-Type", "application/json");
            con.setDoOutput(true); // Enable output to send a body

            String jsonInputString = "{\"user_id\": \"string\", \"is_admin\": true, \"can_upload\": true}";

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
const url = 'http://localhost/api_v2/library/123e4567-e89b-12d3-a456-426614174000/edit_user';

const data = {
  user_id: "string",
  is_admin: true,
  can_upload: true
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
  'http://localhost/api_v2/library/123e4567-e89b-12d3-a456-426614174000/edit_user' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "user_id": "string",
  "is_admin": true,
  "can_upload": true
}'
```

> The above request, on a successful request, returns JSON structured like this:

```json
"string
```

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 422 | Validation Error |

## Create Document

**Summary:** Create Document

### HTTP Request 
`***POST*** /api_v2/library/{library_id}/file` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| library_id | path |  | Yes |  |

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

> The above request, on a successful request, returns JSON structured like this:

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

**Responses**

| Code | Description |
| ---- | ----------- |
| 201 | Successful Response |
| 422 | Validation Error |

## Create Link

**Summary:** Create Link

### HTTP Request 
`***POST*** /api_v2/library/{library_id}/link` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| library_id | path |  | Yes |  |

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

**Responses**

| Code | Description |
| ---- | ----------- |
| 201 | Successful Response |
| 422 | Validation Error |

## Get Documents By Library

**Summary:** Get Documents By Library 

### HTTP Request 
`***GET*** /api_v2/library/{library_id}/documents` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| library_id | path |  | Yes |  |
| skip | query |  | No |  |
| limit | query |  | No |  |

```python
import requests

url = 'http://localhost/api_v2/library/123e4567-e89b-12d3-a456-426614174000/documents?skip=0&limit=100'
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
        String url = "http://localhost/api_v2/library/123e4567-e89b-12d3-a456-426614174000/documents?skip=0&limit=100";

        try {
            HttpURLConnection con = (HttpURLConnection) new URL(url).openConnection();
            con.setRequestMethod("GET");
            con.setRequestProperty("Accept", "application/json");

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
                System.out.println("GET request failed. Response Code: " + responseCode);
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

```

```javascript
const url = 'http://localhost/api_v2/library/123e4567-e89b-12d3-a456-426614174000/documents?skip=0&limit=100';

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
  'http://localhost/api_v2/library/123e4567-e89b-12d3-a456-426614174000/documents?skip=0&limit=100' \
  -H 'accept: application/json'
```

> The above request, on a successful request, returns JSON structured like this:

```json
{
  "documents": [
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
  ],
  "count": 0,
  "page_count": 0
}
```

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 422 | Validation Error |

## Create New Transaction

**Summary:** Create New Transaction

### HTTP Request 
`***POST*** /api_v2/library/{library_id}/transaction` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| library_id | path |  | Yes |  |

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

> The above request, on a successful request, returns JSON structured like this:

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

**Responses**

| Code | Description |
| ---- | ----------- |
| 201 | Successful Response |
| 422 | Validation Error |

# Transaction API
## Generate Text

**Summary:** Generate Text

### HTTP Request 
`***POST*** /api_v2/transaction/generate_text/{transaction_id}` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| transaction_id | path |  | Yes |  |

```python
import requests
import json

url = 'http://localhost/api_v2/transaction/generate_text/123e4567-e89b-12d3-a456-426614174000'
headers = {
    'accept': 'application/json',
    'Content-Type': 'application/json'
}
data = {
    "transaction_ids": [],
    "qa_task": ("Based on the retrieved contexts generate a detailed response to user prompt with in-text citations. "
                "give explanations wherever applicable.\nMake sure to include in-text citations after every 1-2 sentence as '[x]'. "
                "x being the context number from which the information is used. Respond in Markdown format when applicable, "
                "use appropriate markdown syntax for formatting like headings (#, ##, ...), bold, italics etc.\n"
                "If question / user prompt cannot be answered by the contexts, return 'I am unable to answer question based on fetched information'. "
                "Don't try to make up an answer.")
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
        String url = "http://localhost/api_v2/transaction/generate_text/123e4567-e89b-12d3-a456-426614174000";
        String jsonInputString = "{\"transaction_ids\": [], \"qa_task\": \"Based on the retrieved contexts generate a detailed response to user prompt with in-text citations. give explanations wherever applicable.\\nMake sure to include in-text citations after every 1-2 sentence as '[x]'. x being the context number from which the information is used. Respond in Markdown format when applicable, use appropriate markdown syntax for formatting like headings (#, ##, ...), bold, italics etc.\\nIf question / user prompt cannot be answered by the contexts, return 'I am unable to answer question based on fetched information'. Don't try to make up an answer.\"}";

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
const url = 'http://localhost/api_v2/transaction/generate_text/123e4567-e89b-12d3-a456-426614174000';
const data = {
  transaction_ids: [],
  qa_task: "Based on the retrieved contexts generate a detailed response to user prompt with in-text citations. " +
           "give explanations wherever applicable.\nMake sure to include in-text citations after every 1-2 sentence as '[x]'. " +
           "x being the context number from which the information is used. Respond in Markdown format when applicable, " +
           "use appropriate markdown syntax for formatting like headings (#, ##, ...), bold, italics etc.\n" +
           "If question / user prompt cannot be answered by the contexts, return 'I am unable to answer question based on fetched information'. " +
           "Don't try to make up an answer."
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
  'http://localhost/api_v2/transaction/generate_text/123e4567-e89b-12d3-a456-426614174000' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "transaction_ids": [],
  "qa_task": "Based on the retrieved contexts generate a detailed response to user prompt with in-text citations. give explainations whereever applicable.\nMake sure to include in-text citations after every 1-2 sentence as '\''[x]'\''. x being the context number from which the information is used. Respond in Markdown format when applicable, use appropriate markdown syntax for formatting like headings (#, ##, ...), bold, italics etc.\nIf question / user prompt cannot be answered by the contexts, return '\''I am unable to answer question based on fetched information'\''. Don'\''t try to make up an answer."
}'
```

> The above request, on a successful request, returns JSON structured like this:

```json
{
  "transaction_id": "transaction_id",
  "generated_text": "Based on your context, this is the generated text"
}
```

**Responses**

| Code | Description |
| ---- | ----------- |
| 201 | Generate text based on transaction as context |
| 422 | Validation Error |

## Update Transaction

**Summary:** Update

### HTTP Request 
`***PATCH*** /api_v2/transaction/update_answer/{transaction_id}` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| transaction_id | path |  | Yes |  |
| generated_response | query |  | Yes |  |

```python
import requests

url = 'http://localhost/api_v2/transaction/update_answer/123e4567-e89b-12d3-a456-426614174000'
params = {
    'generated_response': '{generated_response}'
}
headers = {
    'accept': 'application/json'
}

response = requests.patch(url, headers=headers, params=params)
print(response.json())

```

```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;

public class Main {
    public static void main(String[] args) {
        String url = "http://localhost/api_v2/transaction/update_answer/123e4567-e89b-12d3-a456-426614174000?generated_response=%7Bgenerated_response%7D";

        try {
            HttpURLConnection con = (HttpURLConnection) new URL(url).openConnection();
            con.setRequestMethod("PATCH");
            con.setRequestProperty("Accept", "application/json");
            con.setDoOutput(true);

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
                System.out.println("PATCH request failed. Response Code: " + responseCode);
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

```

```javascript
const url = 'http://localhost/api_v2/transaction/update_answer/123e4567-e89b-12d3-a456-426614174000';
const params = new URLSearchParams({
  generated_response: '{generated_response}'
});

fetch(`${url}?${params}`, {
  method: 'PATCH',
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
curl -X 'PATCH' \
  'http://localhost/api_v2/transaction/update_answer/123e4567-e89b-12d3-a456-426614174000?generated_response=%7Bgenerated_response%7D' \
  -H 'accept: application/json'
```

> The above request, on a successful request, returns JSON structured like this:

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
        "upload_date": "2024-10-07T22:33:20.031Z",
        "document_url": "string",
        "s3_key": "string",
        "document_id": "string",
        "library_id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
        "account_id": "string",
        "doc_metadata": ""
      }
    }
  ],
  "timestamp": "2024-10-07T22:33:20.031Z",
  "resolution_status": true,
  "feedback": "string",
  "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
}
```

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 422 | Validation Error |

## Pull Transactions

**Summary:** Pull Transactions

### HTTP Request 
`***GET*** /api_v2/transaction/` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| library_id | query |  | Yes |  |
| recent | query |  | Yes |  |
| last_transaction_id | query |  | No |  |

```python
import requests

url = 'http://localhost/api_v2/transaction/'
params = {
    'library_id': '123e4567-e89b-12d3-a456-426614174000',
    'recent': 5,
    'last_transaction_id': '123e4567-e89b-12d3-a456-426614174000'
}
headers = {
    'accept': 'application/json'
}

response = requests.get(url, headers=headers, params=params)
print(response.json())

```

```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;

public class Main {
    public static void main(String[] args) {
        String url = "http://localhost/api_v2/transaction/?library_id=123e4567-e89b-12d3-a456-426614174000&recent=5&last_transaction_id=123e4567-e89b-12d3-a456-426614174000";

        try {
            HttpURLConnection con = (HttpURLConnection) new URL(url).openConnection();
            con.setRequestMethod("GET");
            con.setRequestProperty("Accept", "application/json");

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
                System.out.println("GET request failed. Response Code: " + responseCode);
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

```

```javascript
const url = 'http://localhost/api_v2/transaction/';
const params = new URLSearchParams({
  library_id: '123e4567-e89b-12d3-a456-426614174000',
  recent: 5,
  last_transaction_id: '123e4567-e89b-12d3-a456-426614174000'
});

fetch(`${url}?${params}`, {
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
  'http://localhost/api_v2/transaction/?library_id=123e4567-e89b-12d3-a456-426614174000&recent=5&last_transaction_id=123e4567-e89b-12d3-a456-426614174000' \
  -H 'accept: application/json'
```

> The above request, on a successful request, returns JSON structured like this:

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
          "upload_date": "2024-10-07T22:33:40.535Z",
          "document_url": "string",
          "s3_key": "string",
          "document_id": "string",
          "library_id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
          "account_id": "string",
          "doc_metadata": ""
        }
      }
    ],
    "timestamp": "2024-10-07T22:33:40.535Z",
    "resolution_status": true,
    "feedback": "string",
    "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
  }
]
```

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 422 | Validation Error |

# Feedback
## Submit Feedback

**Summary:** Submit Feedback

### HTTP Request 
`***POST*** /api_v2/feedback/` 

```python
import requests
import json

url = 'http://localhost/api_v2/feedback/'
data = {
    "feedback_type": "string",
    "transaction_id": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
}
headers = {
    'accept': 'application/json',
    'Content-Type': 'application/json'
}

response = requests.post(url, headers=headers, data=json.dumps(data))
print(response.json())

```

```java
import java.io.OutputStream;
import java.net.HttpURLConnection;
import java.net.URL;

public class Main {
    public static void main(String[] args) {
        String url = "http://localhost/api_v2/feedback/";
        String jsonInputString = "{\"feedback_type\": \"string\", \"transaction_id\": \"3fa85f64-5717-4562-b3fc-2c963f66afa6\"}";

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
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

```

```javascript
const url = 'http://localhost/api_v2/feedback/';
const data = {
  feedback_type: 'string',
  transaction_id: '3fa85f64-5717-4562-b3fc-2c963f66afa6'
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
  'http://localhost/api_v2/feedback/' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "feedback_type": "string",
  "transaction_id": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
}'
```

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 422 | Validation Error |

## Read Feedback

**Summary:** Read Feedback

### HTTP Request 
`***GET*** /api_v2/feedback/feedback/{transaction_id}` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| transaction_id | path |  | Yes |  |

```python
import requests

url = 'http://localhost/api_v2/feedback/feedback/123e4567-e89b-12d3-a456-426614174000'
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
        String url = "http://localhost/api_v2/feedback/feedback/123e4567-e89b-12d3-a456-426614174000";

        try {
            HttpURLConnection con = (HttpURLConnection) new URL(url).openConnection();
            con.setRequestMethod("GET");
            con.setRequestProperty("Accept", "application/json");

            int responseCode = con.getResponseCode();
            System.out.println("Response Code: " + responseCode);

            BufferedReader in = new BufferedReader(new InputStreamReader(con.getInputStream()));
            String inputLine;
            StringBuilder response = new StringBuilder();

            while ((inputLine = in.readLine()) != null) {
                response.append(inputLine);
            }
            in.close();

            System.out.println(response.toString());
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

```

```javascript
const url = 'http://localhost/api_v2/feedback/feedback/123e4567-e89b-12d3-a456-426614174000';

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
  'http://localhost/api_v2/feedback/feedback/123e4567-e89b-12d3-a456-426614174000' \
  -H 'accept: application/json'
```

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 422 | Validation Error |

# Authentication


## Validate JSON Web Token

**Summary:** Validate JSON Web Token

### HTTP Request 
`***POST*** /api_v2/authenticate/validatetoken` 


```python
import requests
import json

url = 'http://localhost/api_v2/authenticate/validatetoken'
headers = {
    'accept': 'application/json',
    'Content-Type': 'application/json'
}
data = {
    "sub": "string"
}

response = requests.post(url, headers=headers, data=json.dumps(data))
print(response.json())

```

```java
import java.io.OutputStream;
import java.net.HttpURLConnection;
import java.net.URL;

public class Main {
    public static void main(String[] args) {
        String url = "http://localhost/api_v2/authenticate/validatetoken";
        String jsonInputString = "{\"sub\":\"string\"}";

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
            // You can add code to read the response here if needed.

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

```

```javascript
const url = 'http://localhost/api_v2/authenticate/validatetoken';
const data = {
  sub: "string"
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
  'http://localhost/api_v2/authenticate/validatetoken' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "sub": "string"
}'
```

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 422 | Validation Error |



## Login using email and password


**Summary:** Login using email and password

### HTTP Request 
`***POST*** /api_v2/authenticate/login` 

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 422 | Validation Error |

```python
import requests
import json

url = 'http://localhost/api_v2/authenticate/login'
headers = {
    'accept': 'application/json',
    'Content-Type': 'application/json'
}
data = {
    "email": "string",
    "email_verified": False,
    "given_name": "string",
    "family_name": "string",
    "picture": "string",
    "id": "f7be2192-8182-11ef-8e17-0242ac130003",
    "password": "string",
    "is_superaccount": False
}

response = requests.post(url, headers=headers, data=json.dumps(data))
print(response.json())

```

```java
import java.io.OutputStream;
import java.net.HttpURLConnection;
import java.net.URL;

public class Main {
    public static void main(String[] args) {
        String url = "http://localhost/api_v2/authenticate/login";
        String jsonInputString = "{\"email\":\"string\",\"email_verified\":false,\"given_name\":\"string\",\"family_name\":\"string\",\"picture\":\"string\",\"id\":\"f7be2192-8182-11ef-8e17-0242ac130003\",\"password\":\"string\",\"is_superaccount\":false}";

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
            // You can add code to read the response here if needed.

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

```

```javascript
const url = 'http://localhost/api_v2/authenticate/login';
const data = {
  email: "string",
  email_verified: false,
  given_name: "string",
  family_name: "string",
  picture: "string",
  id: "f7be2192-8182-11ef-8e17-0242ac130003",
  password: "string",
  is_superaccount: false
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
  'http://localhost/api_v2/authenticate/login' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "email": "string",
  "email_verified": false,
  "given_name": "string",
  "family_name": "string",
  "picture": "string",
  "id": "f7be2192-8182-11ef-8e17-0242ac130003",
  "password": "string",
  "is_superaccount": false
}'
```

## Register A User 

**Summary:** Register a user

### HTTP Request 
`***POST*** /api_v2/authenticate/create` 

```python
import requests
import json

url = 'http://localhost/api_v2/authenticate/create'
headers = {
    'accept': 'application/json',
    'Content-Type': 'application/json'
}
data = {
    "email": "string",
    "email_verified": False,
    "given_name": "string",
    "family_name": "string",
    "picture": "string",
    "id": "f7be2192-8182-11ef-8e17-0242ac130003",
    "password": "string",
    "is_superaccount": False
}

response = requests.post(url, headers=headers, data=json.dumps(data))
print(response.json())

```

```java
import java.io.OutputStream;
import java.net.HttpURLConnection;
import java.net.URL;

public class Main {
    public static void main(String[] args) {
        String url = "http://localhost/api_v2/authenticate/create";
        String jsonInputString = "{\"email\":\"string\",\"email_verified\":false,\"given_name\":\"string\",\"family_name\":\"string\",\"picture\":\"string\",\"id\":\"f7be2192-8182-11ef-8e17-0242ac130003\",\"password\":\"string\",\"is_superaccount\":false}";

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
            // You can add code to read the response here if needed.

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

```

```javascript
const url = 'http://localhost/api_v2/authenticate/create';
const data = {
  email: "string",
  email_verified: false,
  given_name: "string",
  family_name: "string",
  picture: "string",
  id: "f7be2192-8182-11ef-8e17-0242ac130003",
  password: "string",
  is_superaccount: false
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
  'http://localhost/api_v2/authenticate/create' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "email": "string",
  "email_verified": false,
  "given_name": "string",
  "family_name": "string",
  "picture": "string",
  "id": "f7be2192-8182-11ef-8e17-0242ac130003",
  "password": "string",
  "is_superaccount": false
}'
```

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 422 | Validation Error |

# Document 
## Get Doc Status 

**Summary:** Get Siblings

### HTTP Request 
`***GET*** /api_v2/document/{doc_id}/check_doc_status` 

```python
import requests

url = 'http://localhost/api_v2/document/30900a6b-ab58-4a3a-b2f8-2d7bd2cd38d0/check_doc_status?word_count=0'
headers = {
    'accept': 'application/json',
    'Authorization': 'Bearer <auth-token>'
}

response = requests.get(url, headers=headers)
print(response.status_code)
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
            String url = "http://localhost/api_v2/document/30900a6b-ab58-4a3a-b2f8-2d7bd2cd38d0/check_doc_status?word_count=0";
            URL obj = new URL(url);
            HttpURLConnection con = (HttpURLConnection) obj.openConnection();
            con.setRequestMethod("GET");
            con.setRequestProperty("Accept", "application/json");
            con.setRequestProperty("Authorization", "Bearer <auth-token>");

            int responseCode = con.getResponseCode();
            System.out.println("Response Code: " + responseCode);

            BufferedReader in = new BufferedReader(new InputStreamReader(con.getInputStream()));
            String inputLine;
            StringBuffer response = new StringBuffer();

            while ((inputLine = in.readLine()) != null) {
                response.append(inputLine);
            }
            in.close();

            System.out.println(response.toString());

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

```

```javascript
const url = 'http://localhost/api_v2/document/30900a6b-ab58-4a3a-b2f8-2d7bd2cd38d0/check_doc_status?word_count=0';
const headers = {
  'Accept': 'application/json',
  'Authorization': 'Bearer <auth-token>'
};

fetch(url, { method: 'GET', headers: headers })
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error('Error:', error));

```

```shell
curl -X 'GET' \
  'http://localhost/api_v2/document/30900a6b-ab58-4a3a-b2f8-2d7bd2cd38d0/check_doc_status?word_count=0' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer <auth-token>'
```

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| doc_id | path |  | Yes |  |
| word_count | query |  | No |  |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 422 | Validation Error |

## Create Document

**Summary:** Create Document

### HTTP Request 
`***POST*** /api_v2/document/port_file` 

```python
import requests

url = 'http://localhost/api_v2/document/port_file?library_id=7650e878-ec84-44f0-b7b9-c068f67bb41b&doc_idx=2'
headers = {
    'accept': 'application/json',
    'Authorization': 'Bearer <auth-token>'
}

response = requests.post(url, headers=headers)
print(response.status_code)
print(response.json())

```

```java
import java.io.OutputStream;
import java.net.HttpURLConnection;
import java.net.URL;

public class Main {
    public static void main(String[] args) {
        String url = "http://localhost/api_v2/document/port_file?library_id=7650e878-ec84-44f0-b7b9-c068f67bb41b&doc_idx=2";

        try {
            HttpURLConnection con = (HttpURLConnection) new URL(url).openConnection();
            con.setRequestMethod("POST");
            con.setRequestProperty("Accept", "application/json");
            con.setRequestProperty("Authorization", "Bearer <auth-token>");
            con.setDoOutput(true);

            int responseCode = con.getResponseCode();
            System.out.println("Response Code: " + responseCode);

            // You can add code here to read the response if necessary

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

```

```javascript
const url = 'http://localhost/api_v2/document/port_file?library_id=7650e878-ec84-44f0-b7b9-c068f67bb41b&doc_idx=2';

const headers = {
  'Accept': 'application/json',
  'Authorization': 'Bearer <auth-token>'
};

fetch(url, {
  method: 'POST',
  headers: headers
})
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error('Error:', error));

```

```shell
curl -X 'POST' \
  'http://localhost/api_v2/document/port_file?library_id=7650e878-ec84-44f0-b7b9-c068f67bb41b&doc_idx=2' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer <auth-token>' \
  -d ''
```

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| library_id | query |  | Yes |  |
| doc_idx | query |  | Yes |  |

**Responses**

| Code | Description |
| ---- | ----------- |
| 201 | Successful Response |
| 422 | Validation Error |

## Get Document

**Summary:** Get Document

### HTTP Request 
`***GET*** /api_v2/document/{doc_id}` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| doc_id | path |  | Yes |  |

```python
import requests

url = 'http://localhost/api_v2/document/7650e878-ec84-44f0-b7b9-c068f67bb41b'
headers = {
    'accept': 'application/json',
    'Authorization': 'Bearer <auth-token>'
}

response = requests.get(url, headers=headers)
print(response.status_code)
print(response.json())

```

```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;

public class Main {
    public static void main(String[] args) {
        String url = "http://localhost/api_v2/document/7650e878-ec84-44f0-b7b9-c068f67bb41b";

        try {
            HttpURLConnection con = (HttpURLConnection) new URL(url).openConnection();
            con.setRequestMethod("GET");
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
const url = 'http://localhost/api_v2/document/7650e878-ec84-44f0-b7b9-c068f67bb41b';

const headers = {
  'Accept': 'application/json',
  'Authorization': 'Bearer <auth-token>'
};

fetch(url, {
  method: 'GET',
  headers: headers
})
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error('Error:', error));

```

```shell
curl -X 'GET' \
  'http://localhost/api_v2/document/7650e878-ec84-44f0-b7b9-c068f67bb41b' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer <auth-token>'

```

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 422 | Validation Error |

## Delete Document

**Summary:** Delete Document

### HTTP Request 
`***DELETE*** /api_v2/document/{doc_id}/delete` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| doc_id | path |  | Yes |  |

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

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 422 | Validation Error |

## Process Document

**Summary:** Process Document

### HTTP Request 
`***POST*** /api_v2/document/{doc_id}/process` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| doc_id | path |  | Yes |  |
| name | query |  | No |  |
| status | query |  | No |  |

```python
import requests

url = 'http://localhost/api_v2/document/7650e878-ec84-44f0-b7b9-c068f67bb41b/process?name=name&status=status'
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
        String url = "http://localhost/api_v2/document/7650e878-ec84-44f0-b7b9-c068f67bb41b/process?name=name&status=status";

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
const url = 'http://localhost/api_v2/document/7650e878-ec84-44f0-b7b9-c068f67bb41b/process?name=name&status=status';

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
  'http://localhost/api_v2/document/7650e878-ec84-44f0-b7b9-c068f67bb41b/process?name=name&status=status' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer <auth-token>' \
  -d ''
```

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 422 | Validation Error |

## Update Document

**Summary:** Update Document

### HTTP Request 
`***POST*** /api_v2/document/{doc_id}/update` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| doc_id | path |  | Yes |  |
| name | query |  | Yes |  |

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

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 422 | Validation Error |

## Get Document

**Summary:** Get Document

### HTTP Request 
`***GET*** /api_v2/document/{doc_id}/page` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| doc_id | path |  | Yes |  |
| page | query |  | No |  |
| answer_id | query |  | No |  |

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

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 422 | Validation Error |

## Get Pending Invitations

**Summary:** Get Pending Invitations

### HTTP Request 
`***GET*** /api_v2/notification/pending_invitations` 

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |

```python
import requests

url = 'http://localhost/api_v2/notification/pending_invitations'
headers = {
    'accept': 'application/json',
    'Authorization': 'Bearer <auth-token>'
}

response = requests.get(url, headers=headers)
print(response.status_code)
print(response.json())  # If you want to print the JSON response

```

```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;

public class Main {
    public static void main(String[] args) {
        String url = "http://localhost/api_v2/notification/pending_invitations";

        try {
            HttpURLConnection con = (HttpURLConnection) new URL(url).openConnection();
            con.setRequestMethod("GET");
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
const url = 'http://localhost/api_v2/notification/pending_invitations';

const headers = {
  'Accept': 'application/json',
  'Authorization': 'Bearer <auth-token>'
};

fetch(url, {
  method: 'GET',
  headers: headers
})
  .then(response => {
    console.log('Response Code:', response.status);
    return response.json();  // If you want to parse the JSON response
  })
  .then(data => console.log(data))
  .catch(error => console.error('Error:', error));

```

```shell
curl -X 'GET' \
  'http://localhost/api_v2/notification/pending_invitations' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer <auth-token>'

```

# Subscription

## Read Subscriptions 

**Summary:** Read Subscriptions

**Description:** Retrieve subscriptions.

### HTTP Request 
`***GET*** /api_v2/subscription/` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| skip | query |  | No |  |
| limit | query |  | No |  |

```python
import requests

url = 'http://localhost/api_v2/subscription/?skip=0&limit=10'
headers = {
    'accept': 'application/json',
    'Authorization': 'Bearer <auth-token>'
}

response = requests.get(url, headers=headers)
print(response.status_code)
print(response.json())  # If you want to print the JSON response

```

```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;

public class Main {
    public static void main(String[] args) {
        String url = "http://localhost/api_v2/subscription/?skip=0&limit=10";

        try {
            HttpURLConnection con = (HttpURLConnection) new URL(url).openConnection();
            con.setRequestMethod("GET");
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
const url = 'http://localhost/api_v2/subscription/?skip=0&limit=10';

const headers = {
  'Accept': 'application/json',
  'Authorization': 'Bearer <auth-token>'
};

fetch(url, {
  method: 'GET',
  headers: headers
})
  .then(response => {
    console.log('Response Code:', response.status);
    return response.json();  // If you want to parse the JSON response
  })
  .then(data => console.log(data))
  .catch(error => console.error('Error:', error));

```

```shell
curl -X 'GET' \
  'http://localhost/api_v2/subscription/?skip=0&limit=10' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer <auth-token>'

```

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 422 | Validation Error |

## Create Subscription 

**Summary:** Create Subscription

**Description:** Create new subscription.

### HTTP Request 
`***POST*** /api_v2/subscription/` 

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 422 | Validation Error |

```python
import requests
import json

url = 'http://localhost/api_v2/subscription/'
headers = {
    'accept': 'application/json',
    'Authorization': 'Bearer <auth-token>',
    'Content-Type': 'application/json'
}

data = {
    "name": "string",
    "description": "string",
    "total_token_limit": 0,
    "allowed_questions_per_day": 0,
    "max_users": 0,
    "library_limit": 0,
    "price": 0,
    "additional_user_price": 0,
    "additional_user_questions_per_day": 0,
    "slug": "string"
}

response = requests.post(url, headers=headers, json=data)
print(response.status_code)
print(response.json())  # If you want to print the JSON response

```

```java
import java.io.BufferedReader;
import java.io.OutputStream;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;

public class Main {
    public static void main(String[] args) {
        String url = "http://localhost/api_v2/subscription/";
        String jsonInputString = "{ \"name\": \"string\", \"description\": \"string\", \"total_token_limit\": 0, \"allowed_questions_per_day\": 0, \"max_users\": 0, \"library_limit\": 0, \"price\": 0, \"additional_user_price\": 0, \"additional_user_questions_per_day\": 0, \"slug\": \"string\" }";

        try {
            HttpURLConnection con = (HttpURLConnection) new URL(url).openConnection();
            con.setRequestMethod("POST");
            con.setRequestProperty("Accept", "application/json");
            con.setRequestProperty("Authorization", "Bearer <auth-token>");
            con.setRequestProperty("Content-Type", "application/json");
            con.setDoOutput(true);

            try (OutputStream os = con.getOutputStream()) {
                byte[] input = jsonInputString.getBytes("utf-8");
                os.write(input, 0, input.length);
            }

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
const url = 'http://localhost/api_v2/subscription/';

const headers = {
  'Accept': 'application/json',
  'Authorization': 'Bearer <auth-token>',
  'Content-Type': 'application/json'
};

const data = {
  "name": "string",
  "description": "string",
  "total_token_limit": 0,
  "allowed_questions_per_day": 0,
  "max_users": 0,
  "library_limit": 0,
  "price": 0,
  "additional_user_price": 0,
  "additional_user_questions_per_day": 0,
  "slug": "string"
};

fetch(url, {
  method: 'POST',
  headers: headers,
  body: JSON.stringify(data)
})
  .then(response => {
    console.log('Response Code:', response.status);
    return response.json();  // If you want to parse the JSON response
  })
  .then(data => console.log(data))
  .catch(error => console.error('Error:', error));

```

```shell
curl -X 'POST' \
  'http://localhost/api_v2/subscription/' \
  -H 'accept: application/json' \
  -H 'Authorization: <auth-token>' \
  -H 'Content-Type: application/json' \
  -d '{
  "name": "string", 
  "description": "string",
  "total_token_limit": 0,
  "allowed_questions_per_day": 0,
  "max_users": 0,
  "library_limit": 0,
  "price": 0,
  "additional_user_price": 0,
  "additional_user_questions_per_day": 0,
  "slug": "string"
}'
```

## Read Subscription By Workspace ID 

**Summary:** Read Subscriptions By Workspace Id

**Description:** Retrieve subscriptions by workspace_id.

### HTTP Request 
`***GET*** /api_v2/subscription/{workspace_id}` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| workspace_id | path |  | Yes |  |
| active | query |  | No |  |

```python
import requests

url = 'http://localhost/api_v2/subscription/7650e878-ec84-44f0-b7b9-c068f67bb41b?active=%3Cactive%3E'
headers = {
    'accept': 'application/json',
    'Authorization': 'Bearer <auth-token>'
}

response = requests.get(url, headers=headers)
print(response.status_code)
print(response.json())  # If you want to print the JSON

```

```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;

public class Main {
    public static void main(String[] args) {
        String url = "http://localhost/api_v2/subscription/7650e878-ec84-44f0-b7b9-c068f67bb41b?active=%3Cactive%3E";

        try {
            HttpURLConnection con = (HttpURLConnection) new URL(url).openConnection();
            con.setRequestMethod("GET");
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
const url = 'http://localhost/api_v2/subscription/7650e878-ec84-44f0-b7b9-c068f67bb41b?active=%3Cactive%3E';

const headers = {
  'Accept': 'application/json',
  'Authorization': 'Bearer <auth-token>'
};

fetch(url, {
  method: 'GET',
  headers: headers
})
  .then(response => {
    console.log('Response Code:', response.status);
    return response.json();  // If you want to parse the JSON response
  })
  .then(data => console.log(data))
  .catch(error => console.error('Error:', error));

```

```shell
curl -X 'GET' \
  'http://localhost/api_v2/subscription/7650e878-ec84-44f0-b7b9-c068f67bb41b?active=%3Cactive%3E' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer <auth-token>'

```

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 422 | Validation Error |

## Get Subscription Stats By Workspace ID 

**Summary:** Get Subscription Stats

**Description:** Retrieve subscription stats by workspace_id.

### HTTP Request 
`***GET*** /api_v2/subscription/stats/{workspace_id}` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| workspace_id | path |  | Yes |  |

```python
import requests

url = 'http://localhost/api_v2/subscription/stats/7650e878-ec84-44f0-b7b9-c068f67bb41b'
headers = {
    'accept': 'application/json',
    'Authorization': 'Bearer <auth-token>'
}

response = requests.get(url, headers=headers)
print(response.status_code)
print(response.json())  # If you want to print the JSON response

```

```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;

public class Main {
    public static void main(String[] args) {
        String url = "http://localhost/api_v2/subscription/stats/7650e878-ec84-44f0-b7b9-c068f67bb41b";

        try {
            HttpURLConnection con = (HttpURLConnection) new URL(url).openConnection();
            con.setRequestMethod("GET");
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
const url = 'http://localhost/api_v2/subscription/stats/7650e878-ec84-44f0-b7b9-c068f67bb41b';

const headers = {
  'Accept': 'application/json',
  'Authorization': 'Bearer <auth-token>'
};

fetch(url, {
  method: 'GET',
  headers: headers
})
  .then(response => {
    console.log('Response Code:', response.status);
    return response.json();  // If you want to parse the JSON response
  })
  .then(data => console.log(data))
  .catch(error => console.error('Error:', error));

```

```shell
curl -X 'GET' \
  'http://localhost/api_v2/subscription/stats/7650e878-ec84-44f0-b7b9-c068f67bb41b' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer <auth-token>'

```

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 422 | Validation Error |

# Payment
## Create an Order


**Summary:** Create Order

### HTTP Request 
`***POST*** /api_v2/payment/workspace/create_order` 

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 422 | Validation Error |

```python
import requests

url = 'http://localhost/api_v2/payment/workspace/create_order'
headers = {
    'accept': 'application/json',
    'Authorization': 'Bearer <auth-token>',
    'Content-Type': 'application/json'
}
data = {
    "name": "string",
    "max_threshold": -1,
    "is_public": False,
    "is_default": False,
    "subscription_slug": "free_tier"
}

response = requests.post(url, headers=headers, json=data)
print(response.status_code)
print(response.json())  # Print the JSON response

```

```java
import java.io.OutputStream;
import java.net.HttpURLConnection;
import java.net.URL;

public class Main {
    public static void main(String[] args) {
        String url = "http://localhost/api_v2/payment/workspace/create_order";

        try {
            HttpURLConnection con = (HttpURLConnection) new URL(url).openConnection();
            con.setRequestMethod("POST");
            con.setRequestProperty("Accept", "application/json");
            con.setRequestProperty("Authorization", "Bearer <auth-token>");
            con.setRequestProperty("Content-Type", "application/json");
            con.setDoOutput(true);

            String jsonInputString = "{ \"name\": \"string\", \"max_threshold\": -1, \"is_public\": false, \"is_default\": false, \"subscription_slug\": \"free_tier\" }";

            try (OutputStream os = con.getOutputStream()) {
                byte[] input = jsonInputString.getBytes("utf-8");
                os.write(input, 0, input.length);
            }

            int responseCode = con.getResponseCode();
            System.out.println("Response Code: " + responseCode);

            // Handle the response

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

```

```javascript
const url = 'http://localhost/api_v2/payment/workspace/create_order';

const headers = {
  'Accept': 'application/json',
  'Authorization': 'Bearer <auth-token>',
  'Content-Type': 'application/json'
};

const data = {
  "name": "string",
  "max_threshold": -1,
  "is_public": false,
  "is_default": false,
  "subscription_slug": "free_tier"
};

fetch(url, {
  method: 'POST',
  headers: headers,
  body: JSON.stringify(data)
})
  .then(response => {
    console.log('Response Code:', response.status);
    return response.json();
  })
  .then(data => console.log(data))
  .catch(error => console.error('Error:', error));

```

```shell
curl -X 'POST' \
  'http://localhost/api_v2/payment/workspace/create_order' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer <auth-token>' \
  -H 'Content-Type: application/json' \
  -d '{
  "name": "string",
  "max_threshold": -1,
  "is_public": false,
  "is_default": false,
  "subscription_slug": "free_tier"
}'

```

## Verify A Payment

**Summary:** Verify Payment

### HTTP Request 
`***POST*** /api_v2/payment/workspace/verify_payment` 

```python
import requests

url = 'http://localhost/api_v2/payment/workspace/verify_payment'
headers = {
    'accept': 'application/json',
    'Authorization': 'Bearer <auth-token>',
    'Content-Type': 'application/json'
}
data = {
    "razorpay_order_id": "string",
    "razorpay_payment_id": "string",
    "razorpay_signature": "string",
    "workspace": {
        "name": "string",
        "max_threshold": -1,
        "is_public": False,
        "is_default": False,
        "subscription_slug": "free_tier"
    }
}

response = requests.post(url, headers=headers, json=data)
print(response.status_code)
print(response.json())  # Print the JSON response

```

```java
import java.io.OutputStream;
import java.net.HttpURLConnection;
import java.net.URL;

public class Main {
    public static void main(String[] args) {
        String url = "http://localhost/api_v2/payment/workspace/verify_payment";

        try {
            HttpURLConnection con = (HttpURLConnection) new URL(url).openConnection();
            con.setRequestMethod("POST");
            con.setRequestProperty("Accept", "application/json");
            con.setRequestProperty("Authorization", "Bearer <auth-token>");
            con.setRequestProperty("Content-Type", "application/json");
            con.setDoOutput(true);

            String jsonInputString = "{ \"razorpay_order_id\": \"string\", \"razorpay_payment_id\": \"string\", \"razorpay_signature\": \"string\", \"workspace\": { \"name\": \"string\", \"max_threshold\": -1, \"is_public\": false, \"is_default\": false, \"subscription_slug\": \"free_tier\" } }";

            try (OutputStream os = con.getOutputStream()) {
                byte[] input = jsonInputString.getBytes("utf-8");
                os.write(input, 0, input.length);
            }

            int responseCode = con.getResponseCode();
            System.out.println("Response Code: " + responseCode);

            // Handle the response

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

```

```javascript
const url = 'http://localhost/api_v2/payment/workspace/verify_payment';

const headers = {
  'Accept': 'application/json',
  'Authorization': 'Bearer <auth-token>',
  'Content-Type': 'application/json'
};

const data = {
  "razorpay_order_id": "string",
  "razorpay_payment_id": "string",
  "razorpay_signature": "string",
  "workspace": {
    "name": "string",
    "max_threshold": -1,
    "is_public": false,
    "is_default": false,
    "subscription_slug": "free_tier"
  }
};

fetch(url, {
  method: 'POST',
  headers: headers,
  body: JSON.stringify(data)
})
  .then(response => {
    console.log('Response Code:', response.status);
    return response.json();
  })
  .then(data => console.log(data))
  .catch(error => console.error('Error:', error));

```

```shell
curl -X 'POST' \
  'http://localhost/api_v2/payment/workspace/verify_payment' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer <auth-token>' \
  -H 'Content-Type: application/json' \
  -d '{
  "razorpay_order_id": "string",
  "razorpay_payment_id": "string",
  "razorpay_signature": "string",
  "workspace": {
    "name": "string",
    "max_threshold": -1,
    "is_public": false,
    "is_default": false,
    "subscription_slug": "free_tier"
  }
}'

```



**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Successful Response |
| 422 | Validation Error |

