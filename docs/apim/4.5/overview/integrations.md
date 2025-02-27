---
description: >-
  Learn more about how Gravitee integrates with your larger enterprise tech
  ecosystem
---

# Integrating Gravitee with other enterprise tooling

## Overview

Gravitee's gateway integrates with a number of different types of enterprise software. These integrations allow users to expose these resources as APIs through the gateway and developer portal. Additionally, Gravitee provides direct and indirect integrations with APM, service discovery, cache, and documentation services.

The following tables summarize major integrations that Gravitee API Management (APIM) offers with other enterprise tooling.

## Event brokers

<table><thead><tr><th width="155.05882352941177">Event broker</th><th width="295">Integration description</th><th>Plugin or add-on required</th></tr></thead><tbody><tr><td>Kafka</td><td>Gravitee can expose backend Kafka data sources as <a href="../using-the-product/managing-your-apis/create-apis/the-api-creation-wizard/">supported client-side APIs.</a></td><td><ul><li>Gateway Kafka Endpoint Connector</li></ul></td></tr><tr><td>Confluent</td><td>Gravitee can expose backend Confluent data sources as <a href="../using-the-product/managing-your-apis/create-apis/the-api-creation-wizard/">supported client-side APIs.</a> Gravitee also supports Confluent Schema registry as a schema validation resource.</td><td><ul><li>Gateway Kafka Endpoint Connector</li><li>Various serialization and deserialization policies</li></ul></td></tr><tr><td>Solace</td><td>Gravitee can expose backend Solace event APIs as <a href="../using-the-product/managing-your-apis/create-apis/the-api-creation-wizard/">supported client-side APIs.</a> Gravitee can also auto-import Solace event APIs.</td><td><ul><li>Management Solace Sync Service plugin</li><li>Gateway Solace Endpoint Connector</li></ul></td></tr><tr><td>HiveMQ</td><td>Gravitee can expose backend MQTT data sources as <a href="../using-the-product/managing-your-apis/create-apis/the-api-creation-wizard/">supported client-side APIs.</a></td><td><ul><li>Gateway MQTT Endpoint Connector</li></ul></td></tr><tr><td>Mosquito</td><td>Gravitee can expose backend MQTT data sources as <a href="../using-the-product/managing-your-apis/create-apis/the-api-creation-wizard/">supported client-side APIs.</a></td><td><ul><li>Gateway MQTT Endpoint Connector</li></ul></td></tr><tr><td>Other MQTT broker running MQTT 5</td><td>Gravitee can expose backend MQTT data sources as <a href="../using-the-product/managing-your-apis/create-apis/the-api-creation-wizard/">supported client-side APIs.</a></td><td><ul><li>Gateway MQTT Endpoint Connector</li></ul></td></tr></tbody></table>

## APM and observability

<table><thead><tr><th width="196.05882352941177">Monitoring solution</th><th>Integration description</th><th>Plugin or add-on required</th></tr></thead><tbody><tr><td>Splunk</td><td>Gravitee can push API metrics and monitoring data to Splunk for visualization in Splunk dashboards.</td><td><ul><li>File reporter plugin</li></ul></td></tr><tr><td>Datadog</td><td>Gravitee can push API metrics and monitoring data to Datadog for visualization in Datadog dashboards.</td><td><ul><li>Datadog reporter plugin</li><li>File reporter plugin (less advanced version)</li></ul></td></tr><tr><td>Dynatrace</td><td>Gravitee can push API metrics and monitoring data to Dynatrace for visualization in Dynatrace dashboards.</td><td><ul><li>File reporter plugin</li></ul></td></tr></tbody></table>

## Service discovery

<table><thead><tr><th width="144">Solution</th><th>Integration description</th><th>Plugin or add-on required</th></tr></thead><tbody><tr><td><a href="../using-the-product/managing-your-apis/api-configuration/v2-api-configuration/service-discovery.md">HashiCorp Consul</a></td><td>Bind the backend endpoints of your API so that API requests are always routed to the proper, healthy backend service dynamically managed by HashiCorp Consul.</td><td><ul><li>Gravitee service discovery consul plugin</li></ul></td></tr></tbody></table>

## API documentation

<table><thead><tr><th width="147.05882352941177">Solution</th><th>Integration description</th><th>Plugin or add-on required</th></tr></thead><tbody><tr><td>Bitbucket</td><td>Fetch content from a Bitbucket repository. Primarily used to fetch documentation.</td><td><ul><li>Bitbucket fetcher plugin</li></ul></td></tr><tr><td>Git</td><td>Fetch content from a Git repository. Primarily used to fetch documentation.</td><td><ul><li>GIT fetcher plugin</li></ul></td></tr><tr><td>GitHub</td><td>Fetch content from a GitHub repository. Primarily used to fetch documentation.</td><td><ul><li>GitHub fetcher plugin</li></ul></td></tr><tr><td>GitLab</td><td>Fetch content from a GitLab repository. Primarily used to fetch documentation.</td><td><ul><li>GitLab fetcher plugin</li></ul></td></tr></tbody></table>

## Authentication and authorization

<table><thead><tr><th width="197.12861736334403">Solution</th><th width="249">Integration description</th><th>Plugin or add-on required</th></tr></thead><tbody><tr><td>Gravitee Access Management</td><td>A Gravitee Access Management resource is defined to introspect an access_token generated by a Gravitee Access Management instance.</td><td><ul><li>Gravitee.io Access Management Resource plugin</li></ul></td></tr><tr><td>Keycloak</td><td>A Keycloak adapter resource is defined to introspect an access token provided by Keycloak.</td><td><ul><li>Keycloak Adapter Resource plugin</li></ul></td></tr><tr><td>OAuth2 authorization servers</td><td>A Generic OAuth2 Authorization Server resource is defined to introspect an access_token generated by a generic OAuth2 authorization server.</td><td><ul><li>Generic OAuth2 Authorization Server Resource</li></ul></td></tr><tr><td>LDAP authentication provider</td><td>A Gravitee LDAP Authentication Provider resource is used to validate a user’s credentials against an LDAP server.</td><td><ul><li>LDAP Authentication Provider plugin</li></ul></td></tr><tr><td>HTTP Authentication provider</td><td>Set up an HTTP authentication provider resource.</td><td><ul><li>HTTP Authentication Provider plugin</li></ul></td></tr><tr><td>Inline authentication</td><td>Set up an inline authentication provider resource (i.e., bring your own users)</td><td><ul><li>Inline Authentication Provider plugin</li></ul></td></tr></tbody></table>

## Cache

<table><thead><tr><th width="157.05882352941177">Solution</th><th width="295">Integration description</th><th>Plugin or add-on required</th></tr></thead><tbody><tr><td>Redis</td><td>The Redis cache resource is used to maintain a cache and link it to the API lifecycle. The cache is initialized when the API is started and released when the API is stopped.</td><td><ul><li>Redis Cache Resource plugin</li></ul></td></tr><tr><td>In-memory cache solution</td><td>The cache resource is used to maintain a cache and link it to the API lifecycle. The cache is initialized when the API is started and released when the API is stopped. This cache is responsible for storing HTTP responses from the backend to avoid subsequent calls.</td><td><ul><li>Cache resource</li></ul></td></tr></tbody></table>

## Custom backend integrations

Flexible API and protocol support enables you to integrate Gravitee with any backend system that can communicate over:

* SOAP
* REST
* WebSocket
* gRPC

{% hint style="info" %}
**For example: Salesforce**

Gravitee can be used for custom Salesforce integration use cases because Salesforce provides streaming APIs. For more information, [book a demo with one of our Solutions Engineers](https://www.gravitee.io/demo).
{% endhint %}
