# API
* signature/token (authentication)
* scopes (authorization)
* find all allowed HTTP request types

## Tools
* [Postman](https://www.getpostman.com/)
* cURL in the terminal

## Signature/token
APIs often use tokens for authentication and
authorization. 
* The token may be manipulated 
  due to leakage of secret used to sign token. If this 
  is the case, you may generate your own token with 
  the right permission. Read about [scopes and roles](#scopes-and-roles).
* [JWT](https://jwt.io) is a new popular token. Read about it!
  * Maybe the developer used Base64 for "encyption". Base64 
  just makes it hard to read, not encrypted. It can easily
  be decrypted.

## Sessions
* Cookies are often used for sessions, maybe take a look
at that?

## Scopes and roles
Scopes and roles are used to set permissions to a user.
Each endpoint in an API that is not publicly open are 
marked with several scopes. Often API documentation has
written down the name of these roles. 
