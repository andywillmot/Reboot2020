# Reboot2020 - OIDC/OAuth Lightning talk

GitHub link:
![GitHub QR Code](https://github.com/andywillmot/Reboot2020/blob/master/QRCode.png "https://github.com/andywillmot/Reboot2020/")

## Definitions - It's all pretty clear!
### OAuth
>An open standard for **access delegation**, commonly used as a way for Internet users to grant websites or applications access to their information on other websites but without giving them the passwords.
### OIDC (OpenID Connect)
>An open standard and decentralized **authentication** protocol promoted by the non-profit OpenID Foundation.  The lastest standard is OpenID Connect 1.0, created as an extension of OAuth 2.0.

![Confused chicken...](https://github.com/andywillmot/Reboot2020/blob/master/confused-chicken.jpg "I'm a bit confused chicken!")
I'm a bit confused chicken.



## A slightly simplistic but 'good enough' way to think about it....
### Authorisation
>The act of giving permission - This is what **OAuth** does
### Authentication
>The act of verifying the identity of a user - This is what **OIDC** extends OAuth to do


## Understanding the history helps

![History](https://github.com/andywillmot/Reboot2020/blob/master/history.jpg "OpenID & OAuth history")

## How the standards work together ##

![Standards map](https://github.com/andywillmot/Reboot2020/blob/master/OpenIDConnect-Map-4Feb2014.png "Standards Map")

## What are the key concepts? ##

### Tokens ###

### Parties ###

Authorisation Server
Relying party

### Grants ###

### Flows ###

## Bring them all together ##

| Spec | OIDC Flow | OAuth Authorization grant type | response_type | openid scope extension? | /authorize response | /token reponse |
|-----------|-----------|--------------------------------------|---------------------|-------------------------|----------------------|--------------------|
| OAuth 2.0 | Auth code | Auth code | code | no | Auth token | Access token |
| OAuth 2.0 | Implicit | Implicit | token | - | Access token | not used |
| OAuth 2.0 | n/a | Resource Owner  Password Credentials | - | no | not used | Access token |
| OAuth 2.0 | n/a | Client Credentials | - | no | not used | Access token |
| OIDC 1.0 | Auth code | Auth code | code | yes | Auth token | ID & Access tokens |
| OIDC 1.0 | Implicit | Implicit | id_token | - | ID token | not used |
| OIDC 1.0 | Implicit | Implicit | id_token token | - | ID & Access tokens | not used |
| OIDC 1.0 | Hybrid | Auth code | code id_token | - | ID & Auth tokens | ID & Access tokens |
| OIDC 1.0 | Hybrid | Auth code & Implicit | code token | yes | Auth & Access tokens | ID & Access tokens |
| OIDC 1.0 | Hybrid | Auth code & Implicit | code token | no | Auth & Access tokens | Access token |
| OIDC 1.0 | Hybrid | Auth code & Implicit | code id_token token | - | ID, Auth & Access  | ID & Access tokens |
| OIDC 1.0 | n/a | n/a | none | doesn't matter | none | none |

## Sources 






