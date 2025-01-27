---
title: Get An Endpoint
menuTitle: Get an Endpoint
weight: 10
aliases:
  - /resources/faq/app-integration
  - /home/resources/faq/app-integration
  - /paths/app-developer/use-ethersjs
  - /home/paths/app-developer/use-ethersjs
  - /paths/app-developer
  - /home/paths/app-developer
  - /home/use/get-endpoint
description: Use the Pocket Portal to "mint" endpoints you can use in your decentralized applications to connect to the blockchain of your choice.
---


In order to take advantage of Pocket's network of thousands of decentralized nodes, you need to create a endpoint that you can use in your application.

You can do this using the **Pocket Portal**.

The [Pocket Portal](https://www.portal.pokt.network) is a free, browser-based application that lets you create (or "mint") and manage endpoints that connect to any blockchain supported by Pocket Network. These endpoints can then be used in any application that expects a connection to an RPC provider.

In this way, the Pocket Portal provides similar functionality to more centralized API services, all while retaining the decentralization that Pocket Network is built on.

Through the Pocket Portal, you can get information about your application usage at a glance, along with network usage, uptime metrics and notifications/alerts.

The Portal is free to use up to one million relays per day.

![](/images/portal.png)
## Create an account

To use the Pocket Portal, you must first create an account.

The Portal accepts two different methods of account creation and authentication: using your email address or your GitHub account.

Once you have an account with one method, you can't switch to another login method with that account, so make sure you choose the method that works best for you.

### Sign up with email

From the main [Pocket Portal](https://www.portal.pokt.network) page:

1. Click Get started at the bottom of the page. Alternatively, you can click **Log In** and then click **Sign Up**.

2. On the sign up page, enter your email address and a password. When done, click **Continue**.

   ![](/images/portal-signup.png)
   {{% notice style="info" %}}
   Your password must contain at least 8 characters, and at least 3 of the following character types: lower case letters, upper case letters, numbers, and special characters. If your password does not meet these requirements, the failing criteria will be displayed on the screen.

   ![](/images/portal-signuppassword.png){{% /notice %}}

3. On the next screen, click **Accept** to authorize the app to allow access to your newly-created account.

   ![](/images/portal-authorize.png)
4. You will then be sent a verification email to the address you entered above. Open this email, and click **Confirm Email Address**.

   ![](/images/portal-emailconfirmation.png)
   {{% notice style="info" %}}
   When you click this link, you will be taken to the main Portal homepage. You will know that verification succeeded because you will receive a subsequent email confirming your registration.
{{% /notice %}}

5. You can now log in. Click the **Log In** button and you will be taken to the Login page. Enter your credentials as previously given and click **Continue**.

Continue below at **Exploring the Portal**.

### Sign up with GitHub

You can also log in the Portal using your existing GitHub account

1. Click **Get started** at the bottom of the page. Alternatively, you can click **Log In** and then click **Sign Up**.

2. Click **Continue with GitHub**.

   ![](/images/portal-signup-github.png)
3. On the next screen, click **Accept** to authorize the app to allow access to your GitHub account.

   ![](/images/portal-authorize.png)
4. You will then be logged in and taken to the Network Overview page. You will also receive an email confirming your registration.

Continue below at **Exploring the Portal**.


## Exploring the Portal

Once you've logged in you'll be taken to the Network Overview section.

![](/images/portal-networkoverview.png)
In this section, you'll see all the important parts of the network: how many relays are being served daily, network performance, the latest block details, and a summary of chains being served by the network is also available.

Click the **Apps** link on the left and then click **Create** to create a new Application. You'll be able to select one of any of the [supported blockchains](/supported-blockchains/) to start, but you can add other chains after your Application is created.

![](/images/portal-app-setup.png)
Once you've hit "Launch Application", your endpoint is ready! You should be greeted by the main application screen, which will show all the metrics, which should will start being populated as soon as you start submitting requests.

![](/images/portal-app.png)
The view you see is the main view for your application. Here, you'll see key details:

* **Endpoint URL**: The endpoint for the chain you selected during creation. Click **Add New** to add new endpoints for different chains that will also be included in this Application. 
* **Portal ID**: Unique identifier for a collection of endpoints generated by the Pocket Portal. It is included as part of the URL of each endpoint.
* **Secret Key**: Security feature for Applications. If "Private Secret Key Required" is selected, then the Secret Key will need to be sent along with the request using HTTP Basic Authentication.
* **Public Key**: Unique identifier for a given Application that will allow you to inspect the Application on-chain.
* **Success metrics**: Relay success rate, error rate, and total requests.
* **Usage**: Percentage of how many relays have been utilized against the maximum (currently one million per day).

## Setting Up Notifications

Turning on notifications is a great way to stay up to date with your app. We respect our users' privacy, and therefore we only send important emails, such as usage notifications. To activate them:

* Click on the "Notifications" button on your app's dashboard, and you'll see the notifications screen.
* Turn on any notifications you're interested in receiving, and then click "Save changes" when you're done.

![](/images/portal-notifications.png)
## Securing your Application

For securing your endpoint, click the **App Security**"** button. This section contains all the security settings you'll have at your disposal for security. We provide whitelisting for both origins and user agents and also let you enable and disable secret key usage.

![](/images/portal-appsecurity.png)
### Whitelisting User-Agents

Mainly useful for mobile apps, whitelisting HTTP User-Agents lets you limit requests to only the ones you've put in the whitelist. An example user agent would be `com.example.bobapp`. This would let Bob's mobile app use the endpoint as his user agent would be whitelisted. If Alice, with user agent `com.example.aliceapp` tried to use the endpoint, she wouldn't be able to, as her requests would be blocked before they're sent to the network.

### Whitelisting Origins

To whitelist origins, just write the URL of the domain you want to allow. All requests from other domains will be blocked. This is a very effective way to only use your app in production, staging, or test environments and to stop malicious users from stealing your endpoint and using it in their project.

For origins, we support wildcard domains as well as normal domains. An example URL would be `https://portal.pokt.network`.

### Using your Secret Key

Every application has a secret key associated with it, which can be enabled so that every request has to send it using [HTTP Basic Authentication](https://developer.mozilla.org/en-US/docs/Web/HTTP/Authentication) to be accepted. An example cURL request with the secret key enabled would be:

{{< tabs >}}
{{% tab name="macOS/Linux" %}}
```
curl --user :YOUR-SECRET-KEY \\
...
https://<NETWORK>.gateway.pokt.network/v1/lb/<YOUR-PORTAL-ID>
```
{{% /tab %}}

{{% tab name="Windows" %}}
```
curl --user :YOUR-SECRET-KEY ^
...
https://<NETWORK>.gateway.pokt.network/v1/lb/<YOUR-PORTAL-ID>
```
{{% /tab %}}
{{< /tabs >}}

This is a truncated example of a call that does not actually send a request. See below for a more detailed example.

## Testing your Endpoint

Once you've set up your endpoint as per your liking, you can test it however you'd like. In the main application view of the dashboard, you'll be able to see and copy your endpoint to the clipboard. The way endpoints are used in terms of content sent in the body will depend on the chain.

For EVM-based chains (Ethereum, BSC, and others), which see the majority of traffic in Pocket Network, you can refer to the official [JSON-RPC](https://ethereum.org/en/developers/docs/apis/json-rpc/#json-rpc-methods) specification. Below we have a few examples of requests for Pocket compatible chains.

### Ethereum, BSC and EVM-based chains

{{< tabs >}}
{{% tab name="macOS/Linux" %}}
```
curl -X POST \\
-H "Content-Type: application/json" \\
--data '{"jsonrpc": "2.0", "id": 1, "method": "eth_blockNumber", "params": []}' \\
"https://<NETWORK>.gateway.pokt.network/v1/lb/<YOUR-PORTAL-ID>"
```
{{% /tab %}}

{{% tab name="Windows" %}}
```
curl -X POST ^
-H "Content-Type: application/json" ^
--data "{\"jsonrpc\": \"2.0\", \"id\": 1, \"method\": \"eth_blockNumber\", \"params\": []}" ^
"https://<NETWORK>.gateway.pokt.network/v1/lb/<YOUR-PORTAL-ID>"
```
{{% /tab %}}
{{< /tabs >}}

### How Endpoints are Constructed

All endpoints have a similar structure, as they all have:

* The network prefix, based on the RelayChainIDs. You can find them on the list of [supported blockchains](/supported-blockchains) in the column **Portal API Prefix**. For example, Ethereum Mainnet is `eth-mainnet`.
* The main URL (`gateway.pokt.network/v1/`)
* If it's a load-balanced endpoint, it will also have the LB prefix (`/lb/`)
* The Portal ID, which is unique to your Application.


## Use EthersJS

You can use Pocket as your node provider with this complete and compact Ethereum library

First, you need to get an endpoint from the [Pocket Portal](https://www.portal.pokt.network).

Then you need to get the Portal ID and use it like this:

```
ethers.providers.PocketProvider('homestead', process.env.GatewayID)
```


## Endpoint FAQ

### I just want an endpoint, where can I get one?

The [Pocket Portal](https://www.portal.pokt.network/) stakes on your behalf and generates the endpoint you need.

### How does the Pocket Portal work?

The Pocket Portal is tasked with connecting to the Pocket Network through PocketJS on your behalf—essentially doing the integration work for you. The only thing that changes here is the layer of abstraction between you, the developer, and the nodes. You are still ultimately being served by a decentralized network of thousands of nodes.

### What does it mean for an endpoint to be "load-balanced"?

This means that there's more than one Application behind your endpoint, where an Application is defined as the account staking into the network for the purpose of submitting relay requests. For each request you need to submit, one of these app stakes gets chosen pseudorandomly and is used to make the request to the network. We have several algorithms in place to cherry-pick the best-performing app stakes for each session, based on the nodes they've been matched with, and ensure the best QoS.

### What can I do if I exceed my allotted requests?

If you ever exceed the amount of daily (or per-session) amount of requests, contact the sales team or jump into our Discord to let us know; we'll work something out!

