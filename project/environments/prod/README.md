# Brightly Flags for `example` project, `prod` environment

> [!WARNING]
> This file is managed by terraform. Do not edit manually.

## `prod` environment description

> Production environment

## Quick Start

If you're reading this, your organization's [Brightly](https://github.com/brightlyorg/brightly/wiki) server should now be available for serving feature flags to your code.
To use those flags, ensure that:
- The correct LaunchDarkly SDK has been added to your application
- The SDK is configured to use your Brightly server

### Adding an SDK to your application

We recommend following the [LaunchDarkly SDK documentation](https://docs.launchdarkly.com/sdk/). In particular:

1. Read [Getting started with SDKs](https://docs.launchdarkly.com/sdk/concepts/getting-started)
1. Choose the [server-side SDK](https://docs.launchdarkly.com/sdk/server-side) or [client-side SDK](https://docs.launchdarkly.com/sdk/client-side) most suitable for your application
1. Follow the instructions to install the SDK and add it to your application
1. To implement the section of the instructions entitled **Initialize the client**, you'll need a [key](https://docs.launchdarkly.com/sdk/concepts/client-side-server-side#keys). Continue to the next section.

### Use the correct key

Server-side SDKs should use this SDK Key:

```
sdk-prod-BK4vjtg0cBWJd22M
```

Client-side SDKs should use this client-side id:
```
prod
```


### Configuring the SDK to use your Brightly server

Please follow the LaunchDarkly documentation for [configuring SDKs to use a Relay Proxy](https://docs.launchdarkly.com/sdk/features/relay-proxy-configuration/proxy-mode).

Find the SDK-specific section for your SDK; it'll contain a code sample in which one or more endpoint URLs are specified. Copy and use this code sample, setting **all** the URLs to:
```
https://brightly-example.mbe39aim2pgh2.us-west-2.cs.amazonlightsail.com/
```

- <details>
  <summary>Example: Configuring a server-side SDK</summary>

  Check out the LaunchDarkly [hello-go example](https://github.com/launchdarkly/hello-go) and modify the config as follows:

  ```golang
      brightlyConfig := ld.Config{
          ServiceEndpoints: ldcomponents.RelayProxyEndpoints("https://brightly-example.mbe39aim2pgh2.us-west-2.cs.amazonlightsail.com/"),
      }

      ldClient, err := ld.MakeCustomClient("sdk-prod-BK4vjtg0cBWJd22M", brightlyConfig, 10*time.Second)
  ```
  </details>

- <details>
  <summary>Example: Configuring a client-side SDK</summary>

  Check out the LaunchDarkly [hello-js example](https://github.com/launchdarkly/hello-js) and modify the config as follows:

  ```javascript
        // Set clientSideID to your environment name
        const clientSideID = 'prod';

        // Set up the evaluation context.
        const context = {
          kind: 'user',
          key: 'example-user-key',
        };

        const options = {
          baseUrl: 'https://brightly-example.mbe39aim2pgh2.us-west-2.cs.amazonlightsail.com/',
          streamUrl: 'https://brightly-example.mbe39aim2pgh2.us-west-2.cs.amazonlightsail.com/',
          eventsUrl: 'https://brightly-example.mbe39aim2pgh2.us-west-2.cs.amazonlightsail.com/',
        };

        const ldclient = LDClient.initialize(clientSideID, context, options);
  ```
  </details>

## Other handy bits
All values below and others are available as terraform outputs for easy wiring into your app.

* Endpoint for this environment: `https://brightly-example.mbe39aim2pgh2.us-west-2.cs.amazonlightsail.com/`
* client-side id: `prod`

### SDK Key
* SDK Key value: `sdk-prod-BK4vjtg0cBWJd22M`
* AWS secret arn: `arn:aws:secretsmanager:us-west-2:310766071441:secret:brightly-example-prod-sdk-key-8MMWI4`
* AWS secret name: `brightly-example-prod-sdk-key`
* AWS: Get secret via cli: `aws secretsmanager get-secret-value --secret-id brightly-example-prod-sdk-key  | jq -r .SecretString`

### Mobile Key
* Mobile Key value: `mob-prod-tQF15KI07DYjptrA`
* Aws secret arn: `arn:aws:secretsmanager:us-west-2:310766071441:secret:brightly-example-prod-mob-key-cdHXqi`
* Aws secret name: `brightly-example-prod-mob-key`
* Get secret using aws cli: `aws secretsmanager get-secret-value --secret-id brightly-example-prod-mob-key  | jq -r .SecretString`

