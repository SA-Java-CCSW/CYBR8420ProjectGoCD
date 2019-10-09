## Assurance Claim - 1: 
**Top Claim 1: GoCD server prevents unauthorized access to its data**
todo: avoid use conjunctive claims, and avoid use features in claims
![Preventions of unauthorized access](https://github.com/SA-Java-CCSW/CYBR8420ProjectGoCD/blob/master/AssuranceClaims/GoCDPreventsUnauthorizedAccess2.png)
* **Evidence E1.1.1:** To gain authorized access to the GoCD Server, user must prove his/her identity via username and password credentials. [User authentication methods](https://docs.gocd.org/19.8.0/configuration/dev_authentication.html) such as password file-based authentication and LDAP server for managing and authentication are used in GoCD. Enabling authentication is one of the first things user should do. 
* **Evidence E1.1.2:** From GoCD server version 19.2.0 onwards, you will be able to create personal access tokens to access GoCD API(s). However, a token can not be used to create or access any access token related API(s). Login using access token is not allowed through web UI. See [Token usage in GoCD](https://docs.gocd.org/19.8.0/configuration/access_tokens.html) for details.
* **Evidence E1.2.1:** Once a user is specified as GoCD Admin, other users will lose their Admin permissions unless they are specified as Admins as well. Only GoCD Admins are able to authorize users with different permissions via its role-based authorization. A role in GoCD is just a group of users which can be assigned with different permissions. Role based access controls and security privileges are very clearly documented in the documentation [Role based access controls page](https://docs.gocd.org/current/configuration/dev_authorization.html).
* **Evidence E1.2.2:** Only GoCD Admins are able to create new pipeline groups and assign specified user or role as Pipeline Group Admins(PGA). PGA has permission to control which users/roles have view/operate/admin permissions for their assigned pipeline group. See [Delegating Group Administration in GoCD](https://docs.gocd.org/19.8.0/configuration/delegating_group_administration.html) for details.
* **Evidence E1.3:** All GoCD APIs require user to authenticate himself/herself using his/her username and password. Starting with version 19.2.0 of GoCD, users may also use a bearer token to authenticate. See [API authentication in GoCD](https://api.gocd.org/current/#authentication) for details.

## Assurance Claim - 2: 
**Top Claim 2:GoCD ensures data consumed from enabling systems is safe from malicious intent**
note: should be more specific
![GoCDExternalDataSourceSafe](https://github.com/SA-Java-CCSW/CYBR8420ProjectGoCD/blob/master/AssuranceClaims/GoCDExternalDataSourceSafe.png)

## Assurance Claim - 3: 
**Top Claim 3: GoCD server protects against malicious plugin**
![Preventions of unauthorized access](https://github.com/SA-Java-CCSW/CYBR8420ProjectGoCD/blob/master/AssuranceClaims/Assurance3.png)
* **Evidence E1.1.1:** Authorized users are allowed to install/remove plugins only when GoCD server restarts. A unique ID is maintained in metadata file for each plugin. GoCD server allows only one plugin of same ID run. 
* **Evidence E1.1.2:** Bundled plugins are developed and supported by Thoughtworks GoCD development team. They will be refreshed with the latest packaged version with an upgrade. However, external plugins will not be upgraded with system upgrade.
* **Evidence E1.2.1:** GoCD server admin users can find all the plugins loaded to  the sever in plugin tab. The plugins' details and status are shown here, including incompatability and validity.
* **Evidence E1.2.2:** authorization plugins installed on GoCD server increases the GoCD server security. 

## Assurance Claim - 4: 
**Top Claim 4: GoCD is sufficiently protected against accidental data loss**

![Preventions of unauthorized access](https://github.com/SA-Java-CCSW/CYBR8420ProjectGoCD/blob/master/AssuranceClaims/Assurance_Claim_4.png)

* **Evidence E.1.1.1:** When GoCD run out of disk space, GoCD notices user with warning box or error message to indicate the server has [run out of disk space](https://docs.gocd.org/current/faq/admin_out_of_disk_space.html), and the schedul has been stopped. GoCD could automatically delete the unused artifacts that occupied space on server. GoCD could also preserve artifacts that are important to the stage by disable deletion of specific artifact from the deleted process.

* **Evidence E.1.2:** By [default](https://docs.gocd.org/current/advanced_usage/dev_clean_up_when_cancel.html), GoCD kills current running tasks and clean up environment for jobs if user already know the jobs are going to fail.  

* **Evidence E.1.3:** To maintain the state inconsistent, GoCD can be indicated to finish certain task during the cleanup process. GoCD allows user to use web interface or XML configuration to perform the [custom cleanup](https://docs.gocd.org/current/advanced_usage/dev_clean_up_when_cancel.html).

## Assurance Claim - 5: 
**Top Claim 5: **

### Project Links
* Team Repository: https://github.com/SA-Java-CCSW/CYBR8420ProjectGoCD
* Project Board: https://github.com/SA-Java-CCSW/CYBR8420ProjectGoCD/projects/3
