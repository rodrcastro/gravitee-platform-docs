# OpenID Connect

## Overview

[OpenID Connect](https://openid.net/connect) allows clients of all types, including web-based, mobile and JavaScript clients, to request and receive information about authenticated sessions and end users.

While OAuth 2.0 is more about accessing resources with opaque tokens, OpenID Connect is about authentication built on top of OAuth 2.0 and using claims to communicate information about the end user.

OpenID Connect provides endpoints and some tools, such as [JSON Web Token (JWT)](https://tools.ietf.org/html/rfc7519), to authenticate and retrieve end-user information.

See the [AM API reference](https://raw.githubusercontent.com/gravitee-io/gravitee-docs/master/am/2.x/oidc/swagger.yml) for OpenID Connect endpoints exposed by AM.

## Protocol

The OpenID Connect protocol workflow is as follows:

1. The RP (client) sends a request to the OpenID Provider (OP).
2. The OP authenticates the end user and obtains authorization.
3. The OP responds with an ID token and usually an access token.
4. The RP can send a request with the access token to the UserInfo Endpoint.
5. The UserInfo Endpoint returns claims about the end user.

{% hint style="info" %}
A `scope` parameter must always be passed using the OAuth 2.0 request syntax containing the `openid` scope value to indicate to the underlying OAuth 2.0 logic that this is an OpenID Connect request.
{% endhint %}

## Flows

### Authorization code flow

The authorization code flow returns an authorization code to the client, which can then exchange it for an ID token and an access token directly. This provides the benefit of not exposing any tokens to the User Agent and possibly other malicious applications with access to the User Agent. The authorization server can also authenticate the client before exchanging the authorization code for an access token. The authorization code flow is suitable for clients that can securely maintain a client secret between themselves and the authorization server.

* Authorization code flow URL: `https://am-gateway/{domain}/oauth/authorize?response_type=code&client_id=web-app&redirect_uri=https://web-app/callback&scope=openid`

### Implicit flow

{% hint style="warning" %}
The OAuth standard now discourages the use of an implicit grant to request access tokens from Javascript applications. You should consider using the Authorization code flow with a PKCE extension for all your applications.
{% endhint %}

When using the implicit flow, all tokens are returned from the [authorization endpoint](https://github.com/gravitee-io/gravitee-platform-docs/tree/main/docs/am/4.2/guides/auth-protocols/oauth-2.0). The token endpoint is not used.

The implicit flow is mainly used by clients implemented in a browser using a scripting language. The access token and ID token are returned directly to the client, which may expose them to the end user and applications that have access to the end user’s User Agent. The authorization server does not perform client authentication.

* Implicit flow URL: `https://am-gateway/{domain}/oauth/authorize?response_type=id_token|id_token+token&client_id=web-app&redirect_uri=https://web-app/callback`

### Hybrid flow

When using the Hybrid flow, some tokens are returned from the authorization endpoint and others are returned from the token endpoint. Hybrid is used by clients who want tokens separately from front channel and back channel.

* Hybrid flow URL: `https://am-gateway/{domain}/oauth/authorize?response_type=code+id_token|code+token|code+id_token+token&client_id=web-app&redirect_uri=https://web-app/callback&scope=openid`

## ID token

The ID token is a security token that contains claims about the authentication of an end user by an authorization server when using a client. The ID token is represented as a JSON Web Token (JWT) and contains user information like username, email address, name, address and so on. ID tokens are digitally signed to create secure exchanges between two parties.

{% hint style="info" %}
In order to get an ID Token, the client must use an authorization code flow or implicit grant with scope `openid` or use an implicit/hybrid flow.
{% endhint %}

## Dynamic client registration

For an OpenID Connect Relying Party (client) to use OpenID services, it needs to first register and be known by the OpenID Provider. With dynamic client registration, RPs can self-register by providing information and obtaining, as a result, the required information (`client_id`) to use it. AM follows the [Openid Connect Dynamic Client Registration](https://openid.net/specs/openid-connect-registration-1_0.html) specifications.

Register URL is available through the `registration_endpoint` attribute, under the OpenID connect discovery endpoint, and used to be: `POST https://am-gateway/{domain}/oidc/register`. READ/UPDATE/DELETE can be performed with respectively GET/(PUT or PATCH)/DELETE on the `registration_client_uri` attribute retrieved from the register payload result.

{% hint style="warning" %}
Unlike PATCH, PUT requires you to provide all the client metadata. Omitted fields will be treated as null or empty values.
{% endhint %}
