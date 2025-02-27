# Application

The `Application` custom resource represents the configuration for a Gravitee application. To access Gravitee APIs, consumers must register an application and subscribe to a published API plan. Applications act on behalf of the user to request tokens, provide user identity information, and consume APIs.

## Type of applications

Gravitee applications fall into two main categories:

* **Simple applications:** these are entirely managed and self-contained within Gravitee
<<<<<<< HEAD
* **Web, SPA, Native, and Backend-to-backend applications:** also know as OAuth applications, or OAuth clients, these can only be created if you have activated Dynamic Client Registration in APIM. This way, Gravitee will refer to an external Identity provider (such as Gravitee Access Management, Keycloak or Ping Federate) to request creation of the application. Gravitee will receive the application's client Id and client secret in response. This allows you to setup OAuth and JWT authentication patterns that involve coordinate across the application, gateway, and authorization server.

## Simple applications
=======
* **Web, SPA, Native, and Backend-to-backend applications:** also know as OAuth applications, or OAuth clients, these can only be created if you have activated Dynamic Client Registration in APIM. This way, Gravitee will refer to an external Identity provider (such as Gravitee Access Management, Keycloak or Ping Federate) to request creation of the application. Gravitee will receive the application's client Id and client secret in response. This allows you to setup OAuth and JWT authentication patterns that involve coordinate across the application, gateway, and authorization server.&#x20;

## Simple applications&#x20;
>>>>>>> parent of 87f43e23 (GitBook: No commit message)

The example below shows a simple `Application` custom resource definition:

<pre class="language-yaml"><code class="lang-yaml"><strong>apiVersion: gravitee.io/v1alpha1
</strong>kind: Application
metadata:
  name: simple-application
spec:
  contextRef:
    name: "management-context-1"
  name: "simple-application"
  description: "This is a SIMPLE application, which means it is entirely managed by Gravitee"
  settings:
    app:
      clientId: "my-client-id"
</code></pre>

Here is the same `Application` resource with support for application metadata:

```yaml
apiVersion: gravitee.io/v1alpha1
kind: Application
metadata:
  name: simple-application
spec:
  contextRef:
    name: "management-context-1"
  name: "simple-application"
  description: "This is a SIMPLE application, which means it is entirely managed by Gravitee"
  settings:
    app:
      clientId: "my-client-id"
  metadata:
  - name: "test metadata 1"
    format: "STRING"
  - name: "test metadata 2"
    format: "STRING"
```

## OAuth applications

These are the application types that require Dynamic Client Registration to be activated in APIM.

Below is an example of a `web` application type CRD:

```yaml
apiVersion: gravitee.io/v1alpha1
kind: Application
metadata:
  name: web-application
spec:
  contextRef:
    name: "management-context-1"
  name: "web-application"
  description: "K8s WEB application"
  domain: "https://example.com"
  settings:
    oauth:
      applicationType: WEB
      redirectUris:
        - "https://example.com"
      grantTypes:
        - authorization_code
  metadata:
  - name: "test metadata 1"
    format: "STRING"
  - name: "test metadata 2"
    format: "STRING"
```

You cannot provide a custom client Id as part of the creation of a `web` application, because it will be generated by the external identify provider configured as part of APIM's Dynamic Client Registration settings.

## The `Application` lifecycle

The following workflow is applied when a new `Application` resource is added to the cluster:

1. The GKO listens for `Application` resources.
2. The GKO resolves any references to external sources such as ConfigMaps or Secrets.
3. The GKO performs required changes, such as adding default settings.
4. The GKO converts the data to JSON format.
5. The GKO compares the definition to the existing definition. If something has changed, the GKO pushes the definition to the Management API (if a `ManagementContext` resource is provided).

The `Application` resource has a `Processing Status` field that makes it possible to view the status of the resource in the cluster. The following `Processing Status` field values are possible:

| Status      | Description                                                                                                                              |
| ----------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| \[None]     | The application has been created but not processed yet.                                                                                  |
| Completed   | The application has been created or updated successfully.                                                                                |
| Reconciling | The operator has encountered a recoverable error. A retry will be performed every 5 seconds until the cluster retry limit is reached.    |
| Failed      | The operator has encountered an unrecoverable error. These are errors that require manual action to correct. No retry will be performed. |

Events are added to the resource as part of each action performed by the operator. To view these events, ensure that the CRD creation steps described above are completed, then run the following command:

```sh
kubectl describe -n gravitee application.gravitee.io basic-application
```

Example output is shown below:

```bash
Name:         basic-application
Namespace:    gravitee
[...]
Events:
  Type    Reason          Age   From                      Message
  ----    ------          ----  ----                      -------
  Normal  AddedFinalizer  73s   application-controller  Added Finalizer for the Application
  Normal  Creating        73s   application-controller  Creating Application
  Normal  Created         72s   application-controller  Created Application
```

For more information:

* The `Application` CRD code is available on [GitHub](https://github.com/gravitee-io/gravitee-kubernetes-operator/blob/master/api/v1alpha1/application_types.go).
* The `Application` CRD API reference is documented [here](../../reference/api-reference.md).
