---
title: "Using Fetch method JavaScript"
seoTitle: "What is fetch api"
seoDescription: "What is fetch api. Using Fetch api in JavaScript"
datePublished: Tue May 16 2023 10:10:49 GMT+0000 (Coordinated Universal Time)
cuid: clhq45nxo000h09jq7mebel0w
slug: using-fetch-method-javascript
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1684231752295/f03ea7d1-5911-4378-9906-ae46c06b66b8.png
tags: api, javascript, frontend, web-development, vanilla-js-1

---

To understand how to use fetch(), First, we have to understand what it does. As per the name stands the fetch API is used to asynchronously fetch data. It provides a JavaScript interface for accessing and manipulating parts of the [HTTP pipeline](https://developer.mozilla.org/en-US/docs/Web/HTTP/Connection_management_in_HTTP_1.x), such as requests and responses. It’s similar to [XMLHttpRequest](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest). But fetch API provides the fetch() method that’s easier to use for getting requests asynchronously.

> `fetch()` allows you to make network requests similar to [XMLHttpRequest](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest) (XHR). The main difference is that the Fetch API uses [Promises](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise), which enables a simpler and cleaner API, avoiding callback hell and having to remember the complex API of [XMLHttpRequest](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest).

#### Using Fetch()

Getting started with fetch is really easy. First of all, you need an URL, in this case, I’m using a fake API from [req.res.in](https://req.res.in) which will generate fake data. To run the command open a simple javascript file and run it in the browser.

If we run that we can see on the console that it’s returning a Promise.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684230766888/e2d41015-e5ec-4a9c-8683-7f36876521d4.png align="left")

Since fetch() is promise based, you can use async-await or .then() and .catch() to fetch the data also. Now, we’re using .then() method to get the response object as follows

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684230768494/20fafce5-83dc-4b00-9b53-534306a5bd8c.png align="left")

which will return our response object as below.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684230769825/da5b35c8-7b3f-46bc-ab0c-2316442ddb77.png align="left")

So, you can see that we’re getting a response with a status code of (200) “OK”. That means the request has succeeded. The body contains all of our data. But we can’t read the data right now. First, we must convert this to a JSON object using the .json() method. This will return another promise so, we’ve to use another .then() method and pass the data into it.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684230771515/8a973ecc-ab55-4a6a-b330-778a04caa216.png align="left")

And then we can see in our console panel our data like below.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684230772946/cf389f96-eab5-427f-a18c-a68849e48a46.png align="left")

For that, we can easily get out data using fetch API.

#### ERROR Handling in Fetch()

To handle the error we use .catch() method to get the error message out with an error status code.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684230775000/6961ddd7-7e0c-4047-a38c-4b24ff4faa6a.png align="left")

#### Modifying Data Using Fetch()

Since now we are getting the data as a response. What if we wanted to modify our data? We need “POST” or “PUT” requests to create or replace data to do that. To use this type of request we have to pass the method as a second argument in the fetch() method. As the third argument, we’ve to enter the Headers object. Inside the headers object we’ve to enter the ‘[content-type’](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Type)

> The `**Headers**` interface of the [Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API) allows you to perform various actions on [HTTP request and response headers](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers). These actions include retrieving, setting, adding to, and removing headers from the list of the request's headers.

And then we have to write the data we want to create or modify as the next argument . But this will generate an error. Because the data we get as a JSON object, to sync the data correctly with the json object we’ve to use json.stringify() to convert it into a string.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684230776739/37c8066d-40e1-4ad0-9b94-b7f036e4d93c.png align="left")

In the above code, I created a POST request to create a name of “Sankalan” using the fetch() method which gives the below response:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684230778366/28975f0a-b2f7-445a-bba1-c808e3566f68.png align="left")

Here you can see youre getting a user with that specified name into the data.

#### Conclusion:

In this way, you can use fetch API to get the data or modify, create, delete the data using the fetch() method. Here are some more resources to learn:

1. [HTTP](https://developer.mozilla.org/en-US/docs/Web/HTTP)
    
2. [HTTP Status Codes](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status)
    
3. [HTTP Request Methods](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods)
    
4. [Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)
    
5. [Using Fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch)
    
6. [Working with the Fetch API](https://developers.google.com/web/ilt/pwa/working-with-the-fetch-api)
    

Thank you!