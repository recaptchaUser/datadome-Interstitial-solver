# Solving the DataDome Interstitial (5s Challenge)

## Understanding the DataDome Interstitial
Before delving into the solution, it's essential to acquaint yourself with the appearance of the DataDome Interstitial. Here's a visual representation:

![DataDome Interstitial Example](https://assets.capsolver.com/prod/images/post/2023-11-21/da75346e-4300-451b-a80d-f0d78670db87.png)

## Prerequisites for Success
Before attempting to tackle the DataDome Interstitial, there are specific requirements and critical considerations to take into account:

### Requirements:
- A Capsolver Key
- A Proxy, with MetaProxies being a recommended choice ([https://metaproxies.net/](https://metaproxies.net/))

### Key Points to Note:
- **Dynamic Query Parameters**: It's imperative that the captcha URL query parameters are dynamic; static URLs won't work.
- **Specific Query Parameters**: The 't' parameter in the URL must be either 'it' (for the Interstitial page) or 'fe' (for the captcha). If it's 'bv', it signifies a ban.
- **Matching TLS**: Ensure that the TLS version matches the Chrome version used, along with the header and its order.
- **Consistent Proxy Usage**: Use the same proxy for both solving the captcha and interacting with the webpage.

Understanding these key points is pivotal for a successful resolution of the DataDome Interstitial using Capsolver.

### Documentation:
To get started, familiarize yourself with the Capsolver documentation: [Capsolver Documentation](https://docs.capsolver.com/guide/antibots/datadome.html).

### The Approach:
For this process, we will employ the `createTask` method, which is elaborated in the image below:
![CreateTask Method](https://assets.capsolver.com/prod/images/post/2023-05-11/3f9e93fd-ecdb-45d8-8c81-aff582c5b6fc.png)

Our focus will be on the required parameters, utilizing the **DatadomeSliderTask** as an example.

## Step-by-Step Guide to Solve DataDome

### ☀️ Step 1: Submitting Information to Capsolver
Commence the process by utilizing the `createTask` method to submit your information:

```JSON
POST https://api.capsolver.com/createTask

{
  "clientKey": "Your_API_KEY",
  "task": {
    "type": "DatadomeSliderTask",
    "websiteURL": "https://antoinevastel.com/bots/datadome",
    "captchaUrl": "https://geo.captcha-delivery.com/captcha/?initialCid=yourInitialCid&cid=yourCid&t=it&referer=https%3A%2F%2Fantoinevastel.com%2Fbots%2Fdatadome&s=YourSParam&e=youreParam",
    "proxy": "yourproxy",
    "userAgent": "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/110.0.0.0 Safari/537.36"
  }
}
```

### 🎯 Step 2: Retrieving the Results
Subsequently, continuously monitor the `getTaskResult` API endpoint until the captcha is successfully solved:

```json
POST https://api.capsolver.com/getTaskResult
Host: api.capsolver.com
Content-Type: application/json

{
    "clientKey":"YOUR_API_KEY",
    "taskId": "TASKID_OF_CREATETASK"
}
```

Upon successful resolution, you will receive a response resembling the following:
![Task Result](https://assets.capsolver.com/prod/images/post/2023-05-11/af01f1dd-9a30-46b6-a536-b43129df8d1a.png)

To verify the captcha token, submit the `datadome` cookie with the response value to the site. If the token is rejected, double-check for any missing or incorrect information, ensuring that TLS, headers, and proxy usage are accurate.

