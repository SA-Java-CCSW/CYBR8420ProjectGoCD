## Assurance Claim - 1: 
**Top Claim 1: GoCD prevents unauthorized access to data on GoCD Server**
![Preventions of unauthorized access](https://github.com/SA-Java-CCSW/CYBR8420ProjectGoCD/blob/master/AssuranceClaims/GoCDPreventsUnauthorizedAccess2.png)
* **Evidence E1.1.1:** To gain authorized access to the GoCD Server, user must prove his/her identity via username and password credentials. [User authentication methods](https://docs.gocd.org/19.8.0/configuration/dev_authentication.html) such as password file-based authentication and LDAP server for managing and authentication are used in GoCD. Enabling authentication is one of the first things user should do. 
* **Evidence E1.1.2:** From GoCD server version 19.2.0 onwards, you will be able to create personal access tokens to access GoCD API(s). However, a token can not be used to create or access any access token related API(s). Login using access token is not allowed through web UI. See [Token usage in GoCD](https://docs.gocd.org/19.8.0/configuration/access_tokens.html) for details.
* **Evidence E1.2.1:** Once a user is specified as GoCD Admin, other users will lose their Admin permissions unless they are specified as Admins as well. Only GoCD Admins are able to authorize users with different permissions via its role-based authorization. A role in GoCD is just a group of users which can be assigned with different permissions. Role based access controls and security privileges are very clearly documented in the documentation [Role based access controls page](https://docs.gocd.org/current/configuration/dev_authorization.html).
* **Evidence E1.2.2:** Only GoCD Admins are able to create new pipeline groups and assign specified user or role as Pipeline Group Admins(PGA). PGA has permission to control which users/roles have view/operate/admin permissions for their assigned pipeline group. See [Delegating Group Administration in GoCD](https://docs.gocd.org/19.8.0/configuration/delegating_group_administration.html) for details.
* **Evidence E1.3:** All GoCD APIs require user to authenticate himself/herself using his/her username and password. Starting with version 19.2.0 of GoCD, users may also use a bearer token to authenticate. See [API authentication in GoCD](https://api.gocd.org/current/#authentication) for details.

## Assurance Claim - 2: 
**Top Claim 2:**

## Assurance Claim - 3: 
**Top Claim 3:**

## Assurance Claim - 4: 
**Top Claim 4:**

## Assurance Claim - 5: 
**Top Claim 5:**

### Project Links
* Team Repository: https://github.com/SA-Java-CCSW/CYBR8420ProjectGoCD
* Project Board: https://github.com/SA-Java-CCSW/CYBR8420ProjectGoCD/projects/3
