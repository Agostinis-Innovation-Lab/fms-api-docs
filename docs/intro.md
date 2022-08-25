---
sidebar_position: 1
slug: /
---

# Intro

The API currently serves two purposes:

1. To **provide** generic suggestions for drugs, and whether or not it's on a company's formulary
2. To **receive** logs of how insurance claims are changed due to these suggestions being provided

It is a REST API with two endpoints:

```
  GET       / formulary / [formulary_id] / drug
  POST      / formulary / [formulary_id] / session-log
```

Each client formulary can contain differing lists of drugs and generic suggestions,
hence the need to specify the formulary in the beginning portion of the route.

---

## Methods

As is standard, RESTful APIs use the different HTTP methods to indicate the action to take
on a resource. There are many HTTP methods with RESTful meaning but we're only implementing
two (2) currently:

| HTTP Method | RESTful Action                               |
| ----------- | -------------------------------------------- |
| GET         | Request information related to the resource. |
| POST        | Create a new resource.                       |

---

## Authorization

The API uses the Bearer token authorization scheme.
The token identifies you as a specific API user.
For testing purposes, an API key will be provided for you.
In the future, we will most likely provide a way for API users to login to a portal of some kind and generate new keys.

This key will be sent in the "Authorization" request header. The scheme uses the format:

```
  Bearer {token}
```

So, a JSON example of your header content might look like this:

```
  headers: {
    'Authorization': 'Bearer tlBhkwpz0Ng1ChgkAlsY'
  }
```

The token we will use in practice will be longer for security reasons. (256 bit)

Failure to provide a valid API key will result in a 401 error being returned.

---

## Error Responses

Potential error status codes that can be sent back are:

| Status Code | Meaning                                        |
| ----------- | ---------------------------------------------- |
| `400`         | Client error, server can/will not process      |
| `401`         | Unauthenticated request                        |
| `403`         | Authenticated but not authorized               |
| `404`         | Resource not found                             |
| `405`         | Valid method, but not allowed on that resource |
| `500`         | Internal server error                          |

Source: [MDN Web Documentation](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status)

Responses containing any of these codes will also contain a body with some human-readable
error message information:

```
  {
    message: "This will be some text describing what went wrong."
  }
```
