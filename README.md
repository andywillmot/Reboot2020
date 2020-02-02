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

| ﻿Originating Specification | OIDC Flow type     | OAuth Authorization grant type                 | response_type       | openid scope extension? | /authorize response      | /token reponse     |
|---------------------------|--------------------|------------------------------------------------|---------------------|-------------------------|--------------------------|--------------------|
| OAuth 2.0 RFC6749         | Authorisation code | Authorisation code                             | code                | no                      | Auth token               | Access token       |
| OAuth 2.0 RFC6749         | Implicit           | Implicit                                       | token               | doesn't matter          | Access token             | not used           |
| OAuth 2.0 RFC6749         | n/a                | Resource Owner Password Credentials            | n/a                 | no                      | not used                 | Access token       |
| OAuth 2.0 RFC6749         | n/a                | Client Credentials                             | n/a                 | no                      | not used                 | Access token       |
| Open ID Connect Core 1.0  | Authorisation code | Authorisation code                             | code                | yes                     | Auth token               | ID & Access tokens |
| Open ID Connect Core 1.0  | Implicit           | Implicit                                       | id_token            | doesn't matter          | ID token                 | not used           |
| Open ID Connect Core 1.0  | Implicit           | Implicit                                       | id_token token      | doesn't matter          | ID & Access tokens       | not used           |
| Open ID Connect Core 1.0  | Hybrid             | Authorisation code                             | code id_token       | doesn't matter          | ID & Auth tokens         | ID & Access tokens |
| Open ID Connect Core 1.0  | Hybrid             | Effectively both authorisation code & implicit | code token          | yes                     | Auth & Access tokens     | ID & Access tokens |
| Open ID Connect Core 1.0  | Hybrid             | Effectively both authorisation code & implicit | code token          | no                      | Auth & Access tokens     | Access token       |
| Open ID Connect Core 1.0  | Hybrid             | Effectively both authorisation code & implicit | code id_token token |                         | ID, Auth & Access tokens | ID & Access tokens |
| Open ID Connect Core 1.0  | n/a                | n/a                                            | none                | doesn't matter          |                          |                    |

## Sources 






