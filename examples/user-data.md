---
layout: default
title: User Data Examples
parent: Requests Example
permalink: examples/user-data
nav_order: 0
---

# Layout Utilities
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Parameters

['Get Full User' documentation](/docs/user-data/get-full-user)

This code snippets are made for the endpoint [get-full-user](/docs/user-data/get-full-user) but you can also use them for all the other user-data endpoints by changing the url in the code.
<br/>

## Java examples

Different examples for java


### Java version 8 and plus

#### Imports

```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.io.OutputStream;
import java.net.HttpURLConnection;
import java.net.URL;
import java.nio.charset.StandardCharsets;
```
<br/>

#### Code snippet

```java
final String data = "{\"username\": \"iim_rudy\"}"; // json {"username": "iim_rudy"}

HttpURLConnection connection;
try {
    connection = (HttpURLConnection) new URL("https://api.shockmc.it/v1/userdata/getfulluser").openConnection();
    connection.setRequestMethod("POST");
    connection.setRequestProperty("Content-Type", "application/json; utf-8"); // contents must be json and utf-8
    connection.setDoOutput(true);
    OutputStream stream = connection.getOutputStream();
    stream.write(data.getBytes(StandardCharsets.UTF_8));
    stream.flush();
    stream.close();

    // now we need the response so:
    BufferedReader reader = new BufferedReader(new InputStreamReader(connection.getInputStream()));
    final StringBuilder builder = new StringBuilder();
    String appender;

    while ((appender = reader.readLine()) != null) {
        builder.append(appender);
    }
    reader.close(); // we can close the reader, we don't need it anymore

    String response = builder.toString();
    System.out.println("Java httpURLConnection response --> " + response); // or builder.toString();

} catch (Exception ex) {
    ex.printStackTrace();
}
```
<br>

### Java version 11 and plus


#### Imports

```java
import java.io.IOException;
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;
```
<br/>

#### Code snippet

```java
final String data = "{\"username\": \"iim_rudy\"}"; // json {"username": "iim_rudy"}

HttpClient httpClient = HttpClient.newBuilder().build();
final HttpRequest.BodyPublisher publisher = HttpRequest.BodyPublishers.ofString(data);
HttpRequest request = HttpRequest.newBuilder().uri(URI.create("https://api.shockmc.it/v1/userdata/getfulluser")).POST(publisher).build();

try {
    HttpResponse<String> response = httpClient.send(request, java.net.http.HttpResponse.BodyHandlers.ofString());
     System.out.println("Java11 httpClient response --> "response.body());
} catch (IOException exception) {
    exception.printStackTrace();
} catch (InterruptedException e) {
    e.printStackTrace();
}
```
<br>

### Java with Apache HttpClient library

#### Dependencies

- org.apache.httpcomponents httpclient, version used 4.5.13
<br/><br/>

#### Maven dependency

```xml
<dependency>
    <groupId>org.apache.httpcomponents</groupId>
    <artifactId>httpclient</artifactId>
    <version>4.5.13</version>
</dependency>
```
<br/>

#### Imports

```java
import org.apache.http.HttpResponse;
import org.apache.http.client.methods.HttpPost;
import org.apache.http.entity.ContentType;
import org.apache.http.entity.StringEntity;
import org.apache.http.impl.client.CloseableHttpClient;
import org.apache.http.impl.client.HttpClientBuilder;

import java.io.IOException;
import java.util.Scanner;
```
<br>

#### Code snippet

```java
final String data = "{\"username\": \"iim_rudy\"}"; // json {"username": "iim_rudy"}

final StringEntity entity = new StringEntity(data, ContentType.APPLICATION_FORM_URLENCODED);
final CloseableHttpClient httpClient = HttpClientBuilder.create().build();
final HttpPost request = new HttpPost("https://api.shockmc.it/v1/userdata/getfulluser");

request.setEntity(entity);

HttpResponse response = null;
try {
    response = httpClient.execute(request);
    final Scanner sc = new Scanner(response.getEntity().getContent());
    final StringBuilder builder = new StringBuilder();
    while (sc.hasNext()) {
        builder.append(sc.nextLine());
    }
    System.out.println("Apache HTTPClient Response --> " + builder.toString());
    httpClient.close();
} catch (IOException exception) {
    exception.printStackTrace();
}
```
<br/>

## Javascript Examples

Asynchronous example for Javascript

#### Imports

```javascript
const axios = require('axios').default;
```
<br/>

#### Code snippet

```javascript
async function request(){
  try {
    let res = await axios({
      method: "POST",
      url: "https://api.shockmc.it/v1/userdata/getfulluser",
      data: {
        username: 'iim_rudy'
      }
    });
    return res;
  } catch (err) {
    return err;
  }
}

request()
.then((res) => {
  console.log(res.data);
});
```

<br/>

## Python Examples

Different examples for python

### Python with aiohttp (async)

#### Imports

```python3
import asyncio
import aiohttp
```
<br/>

#### Code snippet

```python3
async def request(**kwargs):
    async with aiohttp.ClientSession() as session:
        async with session.post('https://api.shockmc.it/v1/userdata/getfulluser', json=kwargs) as response:
            return await response.json()

res = asyncio.run(request(username='iim_rudy'))
print(res)
```

<br/>

### Python with requests (sync)

#### Imports

```python3
import requests
```
<br/>

#### Code snippet

```python3
def request(**kwargs):
    res = requests.post('https://api.shockmc.it/v1/userdata/getfulluser', json=kwargs)
    return res.json()

res = request(username='iim_rudy')
print(res)
```

<br/>
