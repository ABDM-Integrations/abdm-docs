---
title: "Deactivate via Aadhaar Otp"
date: 2022-05-07T18:00:04+05:30
weight: 1
draft: false
---

## Deactivate ABHA via Aadhaar Otp

## Overview of the functionality 

- Users may De-activate his/her ABHA (Health ID)

Following will happen (during the deactivation period) if you deactivate your ABHA (Health ID) :

1. You will lose access to all ABDM applications.
2. You will no longer be able to share your health records over the ABDM network.
3. You will no longer be able to share your ABHA (Health ID) at any health facility.


## API Sequence 

The sequence of APIs used via this method is shown in the diagram below.

![Deactivate ABHA via Aadhaar Otp](/abdm-docs/img/De-Activate_ABHA(Health_ID).png)


## API Information Request Response 




**1. Generate the Gateway session**

Bearer token is received as part of respose and should be passed a Authorization token for subsequent API calls.

**URL:** https://dev.ndhm.gov.in/gateway/v0.5/sessions

**Request:** POST  

**Body:**

```json
{
    "clientId": "string",
    "clientSecret": "string",
    "grantType": "client_credentials"
}
```

**Response:** 200 OK

```json
{
    "accessToken": "string",
    "expiresIn": 600,
    "refreshExpiresIn": 1800,
    "refreshToken": "string",
    "tokenType": "bearer"
}
```





**2. Authentication token public certificate. This certificate is also used to encrypt the data.**

**URL:** https://healthidsbx.abdm.gov.in/api/v1/auth/cert

**Request:** GET  

**Parameters:**

- Authorization
string (header)

- X-HIP-ID
string (header)


**Response:** 200  OK

string





**3. Generate Aadhaar OTP on mobile number linked with Aadhar**

Explanation - API accepts Auth Token and Generates OTP on Linked mobile number.

Request Body - Required

Response - API accepts Auth Token and Generates OTP on Linked mobile number. Returns Error for Unauthorized token .

**URL:** https://healthidsbx.abdm.gov.in/api/v2/account/aadhaar/generateOTP

**Request:** POST  

**Parameters:**

- Authorization string (header)

- X-HIP-ID string (header)

- X-Token string (header)


**Body:**

aadharNumberWebOptionalRequestPayload  (body)

```json
{
  "aadhaar": "afcmKRGLmMtGiG701dEXOBY7k0e94Cc+Cknx88lrkOa6uxQbMwDZWnlp2PUsw1uD+gpv3fj6NHBNhtcII3GksVtkLT9bvcz0svYDyUt/x3jTtedXSYgw4b90GTwfLfs1eow056VsOw9HFS/wB8uH5Ysx+QzpL7PxmAY1WOHwOj04sPKN6Dw8XY8vcXovtvZc1dUB+TPAlGGPNu8iqMVPetukysjRxgbNdLLKMxn46rIRb8NieeyuDx1EHa90jJP9KwKGZdsLr08BysrmMJExzTO9FT93CzoNg50/nxzaQgmkBSbu9D8DxJm7XrLzWSUB05YCknHbokm4iXwyYBsrmfFDE/xCDfzYPhYyhtEmOi4J/GMp+lO+gAHQFQtxkIADhoSR8WXGcAbCUj7uTjFsBU/tc+RtvSotso4FXy8v+Ylzj28jbFTmmOWyAwYi9pThQjXnmRnq43dVdd5OXmxIII6SXs0JzoFvKwSk7VxhuLIRYzKqrkfcnWMrrmRgE8xZ6ZLft6O3IeiHb9WA8b/6/qO8Hdd17FKsSF6te59gSpoajS0Ftj2Qb6uEbuDrqQ4BxN33TG561vCbdkh9MoV2nKckOJhdoBy7shjXJSfiRZf0d9DWOot4zlsBD03H6wx94m51Qh+pCGLQIgFn/c+NHzQYo5ZdsuRGM9v+bhHTInI="
}
```

**Response:** 200  OK

```json
{
  "txnId": "a825f76b-0696-40f3-864c-5a3a5b389a83"
}
```


**4. Deactivate the account using mobile or aadhaar otp.**

**URL:** https://healthidsbx.abdm.gov.in/api/v2/account/profile/deactivate


**Request:** POST  

**Parameters:**

- Authorization string (header)

- X-HIP-ID string (header)

- X-Token string (header)


**Body:**

deactivateAccountByOtpWebRequest  (body)

```json
{
  "authMethod": "AADHAAR_OTP",
  "otp": "sw1uD+gpv3fj6NHBNhtcII3GksVtkLT9bvcz0svYDyUt/x3jTtedXSYgw4b90GTwfLfs1eow056VsOw9HFS/wB8uH5Ysx+QzpL7PxmAY1WOHwOj04sPKN6Dw8XY8vcXovtvZc1dUB+TPAlGGPNu8iqMVPetukysjRxgbNdLLKMxn46rIRb8NieeyuDx1EHa90jJP9KwKGZdsLr08BysrmMJExzTO9FT93CzoNg50/nxzaQgmkBSbu9D8DxJm7XrLzWSUB05YCknHbokm4iXwyYBsrmfFDE/xCDfzYPhYyhtEmOi4J/GMp+lO+gAHQFQtxkIADhoSR8WXGcAbCUj7uTjFsBU/tc+RtvSotso4FXy8v+Ylzj28jbFTmmOWyAwYi9pThQjXnmRnq43dVdd5OXmxIII6SXs0JzoFvKwSk7VxhuLIRYzKqrkfcnWMrrmRgE8xZ6ZLft6O3IeiHb9WA8b/6/qO8Hdd17FKsSF6te59gSpoajS0FtQIgFn/c+NHzQYo5ZdsuRGM9v+bhHTInI=",
  "password": "string",
  "reactivationDate": "12/2/2021",
  "reasons": "Official requirement",
  "txnId": "a825f76b-0696-40f3-864c-5a3a5b389a83"
}
```

**Response:** 204  OK



## Postman + Curl Collection 

**Download the Postman Collection** [here](/abdm-docs/Postman/)

**Download the Curls** [here](/abdm-docs/Curls/)



