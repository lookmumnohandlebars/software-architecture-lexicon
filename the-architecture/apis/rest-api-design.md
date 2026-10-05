# Rest API Design

- **Resource-Based**: Reach out over the internat
- **Stateful**: 

[toc]



## Requests

### Basic HTTP request

```
<METHOD> <URL>
GET https://payments.my-company.com/api/orders/1
```

- `GET` -> The **Request Method**, i.e. what's the action being performed on the resource?
- `https://payments.my-company.com/api/orders/1` -> The **URL**, 
- `https://` -> The request **Protocol** - usually https for the http requests
- `payments.my-company.com` -> The **domain** - which is to say the route to the server. In this case `payments` is a sub-domain, my-company is a secondary domain, and `.com` is th
- `/api` -> Optional **directory** for routing requests (e.g. if you have a load balancer or proxy in-front).
- `/orders/1` -> The `path` or `endpoint` indicating which resource is being acted upon.

> [!NOTE]
>
> There is an implicit port in all URL's also



### Request Methods

- `GET` -
- `POST` - 
- `QUERY` - 
- `PATCH` - 
- `PUT` - 

### Resources / Endpoints



**<u>Best Practices</u>**

- **Design To Be Readable**:
- **Use (Plural) Nouns**:
- **Avoid Nesting Where Possible**:
- **Sub Resources**:

### Request Parameters

- **Path Parameters**:
- **Query Parameters**:
- **Request Body**:
- **Request Headers**:









### Routing



### Request Headers

Request headers are key-value (string-string) pairs that describe

| **Header Name**     | **Type**             | **Common Purpose / Usage**                                   | **Example**                                                  |
| ------------------- | -------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **`Authorization`** | Authentication       | Carries credentials (e.g., Bearer tokens, API keys) to authenticate the client to the server. | `Bearer eyJhbGciOi...`                                       |
| **`Content-Type`**  | Content Negotiation  | Specifies the media/MIME type of the request body sent by the client. | `application/json`                                           |
| **`Accept`**        | Content Negotiation  | Tells the server which response content formats/media types the client can handle. | `application/json`                                           |
| **`Host`**          | Connection / Routing | Indicates the domain name of the server and TCP port number on which the request is targeted. | `api.example.com`                                            |
| **`User-Agent`**    | Identification       | Identifies the client software, OS, and version making the request. | `Mozilla/5.0 ...`                                            |
| **`Cookie`**        | Session / State      | Contains stored HTTP cookies previously sent by the server to manage sessions or state. | `session_id=xyz123`                                          |
| **`Origin`**        | Security (CORS)      | Indicates the origin (scheme, domain, port) that initiated a cross-origin fetch request. | `[https://frontend.example.com](https://frontend.example.com)` |





## Responses

### Response Statuses

- `



### Response Compression







## Design Concerns

### Idempotency

| Approach                   | Description                                                  | When to use |      |
| -------------------------- | ------------------------------------------------------------ | ----------- | ---- |
| <u>Idempotency Keys</u>    | Usually using a header, send a request with a scoped key (hash for example) |             |      |
| <u>Database Contraints</u> | Database constraints - preventing duplicate entries - can protect the system |             |      |
| <u>Locking</u>             | If two or more resources might try                           |             |      |
| <u>ETag</u>                |                                                              |             |      |
|                            |                                                              |             |      |



### Long-Lived Patterns

Sometimes a request will want to be long-lived.

| | | 



### Caching

There are three main types of caching



### Pagination



### Request Filtering



### Response Filtering



### Versioning

| **Versioning Method**                   | **Example Request**                                       | **Primary Pros**                                             | **Primary Cons**                                             | **Typical Use Case**                                         |
| --------------------------------------- | --------------------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **URI Path**                            | `GET /v2/payments`                                        | Highly explicit, easy to route at gateway, simple to inspect & test | Violates pure REST principles (multiple URIs for same resource) | Simple to mid-scale APIs, public APIs, microservices         |
| **Query Parameter**                     | `GET /payments?version=2`                                 | Simple to implement, easy to default if omitted              | Harder to route cleanly, parameters can be lost in redirects or caching | Utility services, simple internal APIs, rapid prototyping    |
| **Custom Header**                       | `GET /payments` `Api-Version: 2026-10-01`                 | Keeps URIs clean, decouples versioning from routing path     | Harder to test directly in browser without API tools         | Enterprise service-to-service APIs, clean REST architectures |
| **Accept Header (Content Negotiation)** | `GET /payments` `Accept: application/vnd.company.v2+json` | Purest REST implementation (HATEOAS / Media Type versioning) | Adds complex request parsing, harder to document and generate client SDKs | High-compliance architectures, strict academic REST APIs     |
| **API Key / Account Pinning**           | `GET /payments` `Authorization: Bearer sk_live_123`       | Seamless developer experience; requests work with zero extra headers or path changes | Backend complexity requires transform pipelines to support historical versions per tenant | Payment platforms (e.g., Stripe) and high-stakes B2B SaaS platforms |



### Documentation



### 

## Security Concerns

### Zero-Trust Input

- **Sanitize**: Sanitize all text input for whitespace & potential malicious html or javascript code
- **Validate**: Validate all fields to ensure they are in line with the system.
- **Protect at Data Layer**:
- **Control Forwarding**:

<u>Request Headers</u>

| **Header**                                          | **Purpose & Usage**                                          |
| --------------------------------------------------- | ------------------------------------------------------------ |
| **`Forwarded`** / **`X-Forwarded-For`**             | Identifies the originating client IP address connecting to a web server through an HTTP proxy or load balancer. `Forwarded` (RFC 7239) is the standardized successor to legacy `X-Forwarded-*` headers. |
| **`Sec-Fetch-\*`** (`Site`, `Mode`, `Dest`, `User`) | Metadata sent by modern browsers indicating origin context (e.g., cross-site vs. same-site, script vs. navigation). Crucial for defense-in-depth against CSRF and cross-site leaks. |
| **`X-Client-Cert`** / **`X-SSL-Cert`**              | In Mutual TLS (mTLS) architectures, edge proxies (like NGINX or Envoy) terminate TLS and pass the client certificate details downstream to backend services via this header. |



### Auth



<u>Request Headers</u>



