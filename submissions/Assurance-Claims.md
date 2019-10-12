# GoCD Assurance Claims

## Summary

Assurance Claims increase confidence that GoCD satisfies security requirements of the user. The 5 Assurance Claims are:

* Assurance Claim - 1: GoCD Server prevents unauthorized access to its data.
* Assurance Claim - 2: GoCD ensures a secure network data transfer from a material source repository.
* Assurance Claim - 3: GoCD server protects against malicious plugin.
* Assurance Claim - 4: GoCD is sufficiently protected against accidental data loss.
* Assurance Claim - 5: GoCD server adequately safeguards against Cross-Site Request Forgery (CSRF) attacks.

The Assurance Claims are based around user requirements for a secure system. Each Assurance Claim was made to eliminate doubts that might exist from the user, and identify any security gaps that exist in GoCD.

## Assurance Claim - 1: 

**Top Claim 1: GoCD Server prevents unauthorized access to its data**
![Preventions of unauthorized access](https://github.com/SA-Java-CCSW/CYBR8420ProjectGoCD/blob/master/AssuranceClaims/GoCDPreventsUnauthorizedAccess5.png)
* **Evidence E1.1.1.1:** GoCD does not seem to have security feature to lock user's account for X minutes after N unsuccessful login attempts, which should be implemented in the future.
* **Evidence E1.1.2.1:** GoCD allow its Admin to choose any authentication plugin. See [Authentication in GoCD](https://docs.gocd.org/19.8.0/configuration/dev_authentication.html) for details.
* **Evidence E1.2.1:** Once a user is specified as GoCD Admin, other users will lose their Admin permissions unless they are specified as Admins as well. Only GoCD Admins are able to authorize users with different permissions via its role-based authorization. A role in GoCD is just a group of users which can be assigned with different permissions. Role based access controls and security privileges are very clearly documented in the documentation [Role based access controls page](https://docs.gocd.org/current/configuration/dev_authorization.html).
* **Evidence E1.2.2:** Only GoCD Admins are able to create new pipeline groups and assign specified user or role as Pipeline Group Admins(PGA). PGA has permission to control which users/roles have view/operate/admin permissions for their assigned pipeline group. See [Delegating Group Administration in GoCD](https://docs.gocd.org/19.8.0/configuration/delegating_group_administration.html) for details.
* **Evidence E1.3:** All GoCD APIs require user to authenticate himself/herself using his/her username and password. Starting with version 19.2.0 of GoCD, users may also use a bearer token to authenticate. See [API authentication in GoCD](https://api.gocd.org/current/#authentication) for details.

## Assurance Claim - 2: 
**Top Claim 2:GoCD ensures a secure network data transfer from a material source repository**
note: should be more specific
![GoCDExternalDataSourceSafe](https://github.com/SA-Java-CCSW/CYBR8420ProjectGoCD/blob/master/AssuranceClaims/GoCDExternalDataSourceSafe.png)

## Assurance Claim - 3: 
**Top Claim 3: GoCD server protects against malicious plugin**
![Preventions of unauthorized access](https://github.com/SA-Java-CCSW/CYBR8420ProjectGoCD/blob/master/AssuranceClaims/Assurance3.png)
* **Evidence E3.1.1:** GoCD server validates installed plugins on the following information: structure, metadata (a unique ID), java classes in the jar file (a valid java file should be a public, non-abstract class; have a public default constructor, implement Go-exposed plugin interface, annotated with @Extension). A unique ID is maintained in metadata file for each plugin. GoCD server allows only one plugin of same ID run. This mechanism seems a little bit limited. An Advanced plugin validation mechanism should be built in GoCD.  [Go_Plugins_Basics](https://developer.gocd.org/current/writing_go_plugins/go_plugins_basics.html)
* **Evidence E3.1.2:** GoCD server admin users can find all the plugins loaded to  the sever in plugin tab. The plugins' details and status are shown here, including incompatibility and validity. It helps admin users to fix plugin issues.
* **Evidence E3.2.1:** GoCD server machine can have username/password login protection for local access and remote access which disallows malicious user from accessing server machine. But this is out of GoCD's protection, it depends on how admin users configured the server machine.
* **Evidence E3.2.2:** GoCD server plugin installation folders(bundled and external) are protected with access control, only admin users can modify it. This is also out of GoCD's control, and is completely controlled by server machine's user access control mechanism. 
* **Evidence E3.3.1:** External plugins are not allowed to ungrade when GoCD server is running. Its upgrade procedure is same as its installation procedure which is when GoCD server is stopped. So Evidence E3.1.1, E3.1.2, E3.2.1, E3.2.2 supports here.
* **Evidence E3.3.2:** Bundled plugins are developed and supported by Thoughtworks GoCD development team. They will be refreshed with the latest packaged version with an upgrade.  GoCD doesn’t have much information avoiding malicious plugins download. The plugin validation mechanism supported by GoCD seems limited (Eviendce E3.1.1) as it only validates 

## Assurance Claim - 4: 
**Top Claim 4: GoCD is sufficiently protected against accidental data loss**

![Preventions of unauthorized access](https://github.com/SA-Java-CCSW/CYBR8420ProjectGoCD/blob/Claim4Adjustment/AssuranceClaims/Assurance_Claim_4.png)

* **Evidence E.4.1.1:** When GoCD runs the backup process, GoCD requires user ensure artifacts are manually backed up regularly. See [Running out of disk space](https://docs.gocd.org/current/faq/admin_out_of_disk_space.html#move-the-artifact-repository-to-a-new-larger-drive) for details. GoCD allows users specifically control the artifact purge. The document also points out user needs to manually back up elements such as Log files, plugins, etc. See [Backup GoCD Server](https://docs.gocd.org/current/advanced_usage/one_click_backup.html) for details. 

* **Evidence E.4.2.1:** GoCD requires user restore GoCD backup onto a version that is newer than the version that performs the backup. GoCD provides file version.txt to notice user to perform backup in correct version. See [Backup GoCD Server](https://docs.gocd.org/current/advanced_usage/one_click_backup.html) for more details.

* **Evidence E.4.3.1:** In order to save memory space, by default GoCD will remove all state that related to process which is known is going to fail. However, GoCD provides two alternatives to user to change behavior of removing all state in process. GoCD allows user to use web interface or XML configuration to perform the custom cleanup. See [Clean up after canceling a task]( https://docs.gocd.org/current/advanced_usage/dev_clean_up_when_cancel.html) for more details.

## Assurance Claim - 5: 
**Top Claim 5: GoCD server adequately safeguards against Cross-Site Request Forgery (CSRF) attacks.**

![GoCD server adequately safeguards against CSRF](https://github.com/SA-Java-CCSW/CYBR8420ProjectGoCD/blob/master/AssuranceClaims/GoCDSafegaurdsCSRF.png)


Github has automatic bug tracking that alerts if a dependency has a reported bug.

GoCD has settings that can trigger builds only with user intervention to prevent risk.

### Project Links
* Team Repository: https://github.com/SA-Java-CCSW/CYBR8420ProjectGoCD
* Project Board: https://github.com/SA-Java-CCSW/CYBR8420ProjectGoCD/projects/3
