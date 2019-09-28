## Software Security Requirements - GoCD


### Overview
First, we briefly defined security requirements of GoCD by following environment, data flows, and threat actors were used as the foundation for requirements engineering. Then, we utilized use-cases and misuse-cases for each data flow to described the security requirements. Finally we estimated arrangement of security requirements, security-related configuration and installation issues with different features of GoCD. 

##### Environment 


##### Data Flows
1. Data Flow 1
2. User Creates Value Stream Map (VSM) - *Example: User login GoCD to create end-to-end from commit to deployment workflow or the so-called Value Stream Map (VSM)*
3. Pipeline Locking: Run Instance of Pipeline - *The pipeline is not unlocked if it reaches a manual stage. If a pipeline is locked, it will not allow any new instances to run, unless it is unlocked, either manually or through the API.*
4. Data Flow 4
5. Data Flow 5

##### Threat Actor Examples
There are many threat actors that might want to attack an GoCD Server when it contains valuable software to be deployed.  Threat actors might also want to disrupt the functions that GoCD provides to the software development team.  The following are some examples of threat actors identified for this scenario.
1. Ransomware Authors
2. Malicious Insider User
3. Hacktivist Agents

### Use Cases / Misuse Cases

##### Use Case 1

##### User Creates Value Stream Map (VSM)
![Malicous User Modifies VSM](https://github.com/SA-Java-CCSW/CYBR8420ProjectGoCD/blob/master/MisuseCases/UserCreatesVSM2.png)
GoCD is a best-of-breed tool for Continuous Delivery (CD) which allows a software development team to get changes of all types—including new features, configuration changes, bug fixes and experiments—into production, or into the hands of customers as quickly as possible. The most important use case in GoCD is to let users create an end-to-end from commit to deployment workflow or the so-called Value Stream Map (VSM). VSM helps you visualize your entire CI/CD workflow and allows you to trace a commit from when it is checked in up to when it is deployed. VSM is laid out as an end-to-end dependency graph originating from source control materials and flows from left to right passing various pipelines. Check [GoCD User Documentation](https://docs.gocd.org/current/navigation/value_stream_map.html) for more info. A user must first be assigned as Pipeline Group Administrator for a Pipeline Group created by GoCD System Administrator before he/she can build VSM within that Pipeline group. In the mean time GoCD Pipeline Group Administrator is also responsible for managing permissions of assigned pipeline group. An VSM usually consists of multiple piplelines with dependencies among them. A GoCD pipeline consists of one or more "stages", each stage consists of one or more "jobs" and each job is made up of one or more "tasks". Each stage must run sequentially, but multiple jobs in the same stage are independent of each other and can be run in parallel at the same time. Each task in a job must run sequentially as well. Check [GoCD Get Started Tutorial](https://www.gocd.org/getting-started/part-1/#concept4) for more info about these key concepts in GoCD.

The misuse case mainly focused on modifying the GoCD pipelines and specifying malicious source control materials (SCM) by unauthorized internal Malicious user. Specifying malicious SCMs could threaten normal SCM specification process and could be prevented by managing permissions of the pipeline group. Modifying pipelines without authorization also includes setting Environment variables and creating/modifying tasks in jobs which apparently threatens the normal pipeline creation process. This can be prevented by GoCD System Administrators via configuring user/role based authorization in GoCD. Ways to control user/role based permissions are clearly documented in the [GoCD User Documentation](https://docs.gocd.org/current/configuration/dev_authorization.html). 

Security Requirements
* Role-based access control should be enabled to prevent users from performing unauthorized actions on configuring the entire VSM workflow.
* GoCD Pipeline Group Administrator is responsible for managing permissions of assigned pipeline group to prevent unauthorized users from specifying malicious SCMs. 

GoCD seems to have Role-based access control feature. Role based access controls and security privileges are very clearly documented in their documentation [Role based access controls page](https://docs.gocd.org/current/configuration/dev_authorization.html). 

From my observation, GoCD successfully prevents users from getting unauthorized permissions via its user/role based authorization feature.


##### Use Case 3
![Pipeline Locking: Run Instance of Pipeline](https://github.com/SA-Java-CCSW/CYBR8420ProjectGoCD/blob/master/MisuseCases/RunPipelineInstance.png)
#####  Use Case 4

##### Use Case 5

### Documentation Review
##### Installation Settings
* Security has to be enabled explicitly using one of two GoCD's built-in authentication methods since a newly installed GoCD server does not require users to authenticate. You can choose either Password-file based authentication or LDAP/Active Directory authentication.
* You can also choose from a collection of community-maintained plugins for other methods of authentication, such as using Google or GitHub OAuth.
* Default disabled authentication is great for a trial. However, it is one of the first things you should change, as soon as you decide to use GoCD more widely.
##### General Settings
* When Password-file based authentication is used, the passwords are hashed and stored on GoCD Server. There are a bunch of hashing algorithms to select from such as bcrypt, PBKDF2 and SHA1. It is highly recommended that users use passwords hashed using bcrypt and not SHA1. Passwords can be generated using Apache HTTP Server utility htpasswd such as "htpasswd -c -B /etc/go/password.properties YourChosenUsername". Check [GoCD File-based Authentication Plugin](https://github.com/gocd/gocd-filebased-authentication-plugin#readme) for details.
* Once you have configured basic authentication security, the default is that any user can perform any operation. GoCD allows you to restrict the users who can perform certain functions. Specifying administrators is optional – without it, all users are automatically made administrators. Once a user is specified as administrator, other users will lose their administrator permissions unless they are specified as administrators as well. 
* GoCD supports role-base security. You can define roles that can be used anywhere that authorization is required. A role is just a group of users. For example, you may have 3 pipelines configured as part of your workflow – build, acceptance and deploy. You team may consist of 6 developers and 2 testers. With roles, you can group all 6 of your developers into a role called “developers” and your 2 testers into a role called “testers”. You’d then assign the proper permissions to these pipelines. Check [GoCD User Documentation](https://docs.gocd.org/current/configuration/managing_users.html) for more info.
* From GoCD server version 19.2.0 onwards, you will be able to create personal access tokens to access GoCD API(s). This will allow users to make an API call without specifying their credentials (username & password) as a part of API request headers. Check [GoCD User Documentation](https://docs.gocd.org/current/configuration/access_tokens.html) for more info.

#### TLS/SSL settings
* We can choose which ciphers and SSL/TLS protocols GoCD Server will use for communication with GoCD agents and users (and their browsers). We can configure system properties go.ssl.ciphers.include,	go.ssl.protocols.include etc. in  ${INSTALL_DIR_GO_SERVER}/wrapper-config/wrapper-properties.conf on GoCD Server and configure system property go.ssl.agent.protocol in ${INSTALL_DIR_GO_AGENT}/wrapper-config/wrapper-properties.conf on GoCD Agent. The default transport protocol that agent uses to communicate with Go server is TLSv1.2. 
* The GoCD server on first startup will create a self-signed SSL certificate that is ready for use by you. We may replace GoCD’s certificate with our own following [GoCD User Documentation](https://docs.gocd.org/current/installation/ssl_tls/custom_server_certificate.html).
* The agent by default trusts any and all certificates offered to it, which may possibly allow for MITM attacks. If we’d like to improve security further, by providing our own server certificate, we may add "wrapper.app.parameter.103=-rootCertFile", "wrapper.app.parameter.104=/path/to/root-cert.pem", "wrapper.app.parameter.105=-sslVerificationMode" and "wrapper.app.parameter.106=FULL" in ${INSTALL_DIR_GO_AGENT}/wrapper-config/wrapper-properties.conf before starting the GoCD agent process.

### Project Links
* Team Repository: https://github.com/SA-Java-CCSW/CYBR8420ProjectGoCD
* Project Board: https://github.com/SA-Java-CCSW/CYBR8420ProjectGoCD/projects/2
