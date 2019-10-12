# GoCD Assurance Claims

## Summary

Assurance Claims increase confidence that GoCD satisfies security requirements of the user. The 5 Assurance Claims are:

* Assurance Claim - 1: GoCD Server prevents unauthorized access to its data.
* Assurance Claim - 2: GoCD ensures a secure network data transfer from a material source repository.
* Assurance Claim - 3: GoCD server protects against malicious plugin.
* Assurance Claim - 4: GoCD is sufficiently protected against accidental data loss.
* Assurance Claim - 5: GoCD server adequately safeguards against Cross-Site Request Forgery (CSRF) attacks.

The Assurance Claims are based around user requirements for a secure system. Each Assurance Claim's purpose is to eliminate user doubts that the system is insecure. Analysis of the Assurance Claims will identify any security gaps that exist in GoCD.

Assurance Claim 1 is a necessary assurance case as GoCD is handling data that requires confidentiality and integrity. As a continuous integration and continuous delivery(CI/CD) server, GoCD's features and security mechanisms should increase user confidence the server is preventing unauthorized access to the its data.

Assurance Claim 2 is a necessary assurance case as GoCD accesses out-of-scope enabling systems over the network. Data going between GoCD and its enabling systems are confidential, and require availability for the GoCD to function as intended. 

Assurance Claim 3 is a necessary assurance case as GoCD users will extend the functionality of the server with 3rd party plugins. Users require high trust that the server will not significantly decrease security or introduce security compromises through the use of 3rd party plugins.

Assurance Claim 4 is a necessary assurance case as GoCD must be available and retain data integrity. Low confidence that the GoCD server cannot protect against data loss will not meet user requirements. A CI/CD server must remain operational to test and deploy code. Additionally, a loss in data impacts integrity, and is unacceptable to both the functionality of the server and code that is being deployed.

Assurance Claim 5 is a necessary assurance case as GoCD uses a web application for its front-end interface. Cross-Site Forgery Requests (CSFR) is a common web application weakness which enables an adversary to make function calls to a logged in web application, thereby bypassing the web application's authentication mechanism. User confidence that GoCD has features to safeguard against CSFR attacks is important since the attack vector can adversely effect the confidentiality and integrity of the system if successful.

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

* **Evidence E.2.1.1.1:** Security Gap: There is no indication that GoCD logs any changes to Pipeline setting changes. 

* **Evidence E.2.1.1.2:** Security Gap: Default authorization settings gives all users full access rights until a user is configured as an administrator. See [Authorization Documentation](https://docs.gocd.org/current/configuration/dev_authorization.html). Once a administrator is created, all subsequent users will default to low privilege access rights, only capable of a few functions. A new user will still be able to edit Material source settings. Further configuration would be required.

* **Evidence E.2.1.1.1:** Github has a security alert system that will automatically scan and alert project owners of vulnerable APIs used in the project. See [Github Help](https://help.github.com/en/articles/about-security-alerts-for-vulnerable-dependencies).

* **Evidence E.2.2.1.2:** GoCD is an mature, opensource project sponsered by ThoughtWorks, a software consulting company. The project is collaborated through [Github](https://github.com/GoCD/GoCD/issues) and [development forum](https://groups.google.com/forum/#!forum/go-cd-dev). Further inquiry required about GoCD development process is required. Public collaboration appears to be ad hoc with the official Go Core team leading release efforts. A checklist of items that are introduced into each release [as seen in this forum post](https://groups.google.com/forum/#!searchin/go-cd-dev/release$20plan%7Csort:date/go-cd-dev/zxaoiPNytRI/4Y3NHVFDnmEJ).

* **Evidence E.2.3.1.1:** GoCD will use a self-signed SSL certificate. See [official documentation](https://docs.gocd.org/current/installation/ssl_tls/custom_server_certificate.html).

* **Evidence E.2.3.2.1:** In the event of a flawed SSL/TLS protocol being used by GoCD, GoCD allows the configuration of a self-signed certificate to be used instead. See [this official blog post](https://www.gocd.org/2014/06/05/using-go-cd-with-custom-certificates/) and [official documentation](https://docs.gocd.org/current/installation/ssl_tls/custom_server_certificate.html) that explains how this is performed. Security Gap: There appears to be no indication if a warning message or alert occurs if a insecure certificate is being used in official documentation.

* **Evidence E.2.4:** Material Source settings can be changed for human intervention before the server connects to the enabling system. See [Material Object Documentation](https://api.gocd.org/current/#the-material-object) and [GoCD blog tutorial article](https://www.gocd.org/2018/07/17/gocd-materials-blacklisting-whitelisting/) for extra material polling settings. Security Gap: The setting that requires human intervention is not enabled by default, and must be changed either in the web application gui interface or through GoCD's XML configuration file. 

* **Evidence E.2.5:** Git uses a combination of SSH and SSL/TLS to prevent source spoofing. Security Gap: Material Source is reliant on the capabilities of the enabling system. 

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

**Evidence E.5.1:** GoCD's logins are based on cookie settings. Cookie settings can be changed that enable the logoff to occur after a certain amount of time. Default settings automatically log the user off after 14 days. See [Authentication Documentation](https://docs.gocd.org/current/configuration/dev_authentication.html). Security Gap: For added security, the default setting in configurable properties should be changed to "-1" in "go.sessioncookie.maxage.seconds". This setting will expire the session cookie upon browser close. Expiring the session cookie upon browser close will reduce the likelihood of an CSRF to occur.

**Evidence E.5.2.1.1:** GoCD uses Spring Security for session token generation and authentication. Spring Security is an industry standard security API using best cryptographic security practices. See [Spring Security](https://spring.io/projects/spring-security).

**Evidence E.5.2.1.2:** GoCD uses Spring Security for session token generation and authentication. Spring Security is an industry standard security API using best cryptographic security practices. See [Spring Security](https://spring.io/projects/spring-security).

**Evidence E.5.2.1.3:** GoCD uses Spring Security for session token generation and authentication. Spring Security is an industry standard security API using best cryptographic security practices. See [Spring Security](https://spring.io/projects/spring-security).

**Evidence E.5.3:** GoCD implements [Hackerone](https://hackerone.com/gocd) for a vulnerability disclosure program. This program is used to reduce security weaknesses. A [Github issue](https://github.com/gocd/gocd/issues) is opened up about identified XSS weaknesses and corrected by development.

**Evidence E.5.4:** GoCD uses JRuby on Rails framework for the web application portion of the server. By default, all non-GET requests are not generated with Rails; however, GET requests do not have anti-CSRF applied by default. JRuby on Rails was implemented in release 15. Technical debt might have introduced a security risk. More investigation is required through source code.

### Project Links
* Team Repository: https://github.com/SA-Java-CCSW/CYBR8420ProjectGoCD
* Project Board: https://github.com/SA-Java-CCSW/CYBR8420ProjectGoCD/projects/3
