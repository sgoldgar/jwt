# JWT

To help prepare for API authentication tomorrow, research [JSON Web Tokens](https://jwt.io) (known as JWTs). This should take about 30 minutes. Answer the following questions and submit this README as your homework:

1. What are the 3 parts of a JWT (separated by dots)?
  -Header = type of token + hashing algorithm (usually both) Ex:
  ```
  {
  "alg": "HS256",
  "typ": "JWT"
  }
  ```
  -Payload = claims (which are statements about an entity (typically, the user) and additional metadata)
    -Three types of claims:
      1. Reserved: These is a set of predefined claims which are not mandatory but recommended, to provide a set of useful, interoperable claims. Some of them are: iss (issuer), exp (expiration time), sub (subject), aud (audience), and others.
      2. Public: These can be defined at will by those using JWTs. But to avoid collisions they should be defined in the IANA JSON Web Token Registry or be defined as a URI that contains a collision resistant namespace.
      3. Private: These are the custom claims created to share information between parties that agree on using them.
  Example of payload:
  ```
  {
  "sub": "1234567890",
  "name": "John Doe",
  "admin": true
  }
  ```
  -Signature = To create the signature part you have to take the encoded header, the encoded payload, a secret, the algorithm specified in the header, and sign that. The signature is used to verify that the sender of the JWT is who it says it is and to ensure that the message wasn't changed along the way.
  Example of signature created with HMAC algorithm:
  ```
  HMACSHA256(
  base64UrlEncode(header) + "." +
  base64UrlEncode(payload),
  secret)
  ```

2. What information does each part contain?
See above
3. Why do people use JWTs for authentication? A great resource to read would be https://jwt.io/introduction/.
  -JSON is less verbose than XML and thus its encoded size is smaller and JWT is more compact than SAML. This makes JWT a good choice to be passed in HTML and HTTP environments.

  -Security-wise, SWT can only be symmetrically signed by a shared secret using the HMAC algorithm. However, JWT and SAML tokens can use a public/private key pair in the form of a X.509 certificate for signing. Signing XML with XML Digital Signature without introducing obscure security holes is very difficult when compared to the simplicity of signing JSON.

  -JSON parsers are common in most programming languages because they map directly to objects. Conversely, XML doesn't have a natural document-to-object mapping. This makes it easier to work with JWT than SAML assertions.

  -Regarding usage, JWT is used at Internet scale. This highlights the ease of client-side processing of the JSON Web token on multiple platforms, especially mobile.
