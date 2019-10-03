## Software Security Requirements - GoCD


### Overview
First, we briefly defined security requirements of GoCD by following environment, data flows, and threat actors were used as the foundation for requirements engineering. Then, we utilized use-cases and misuse-cases for each data flow to described the security requirements. Finally we estimated arrangement of security requirements, security-related configuration and installation issues with different features of GoCD. 

##### Environment 
The organization is a large enterprise environment. The organization is transitioning their classical software development methodology to DevOPs. The "DevOps Evangelist", the leader tasked with the project of transiting the organization to DevOps, has created a new team for a software project using DevOPs. The organization is using GoCD as it's continuous development and delivery server. Supporting systems include Github repository, and a Ubuntu webserver for project deployment.

The organization uses the website as a marketing tool for many of it's clients, and used by the organization's marketers throughout the world. The website uses the latest web design practices, and has won numerous awards. The website requires continual updates throughout the to create the biggest viral impact, making the website a perfect candidate to start the organization's DevOP transformation. Although no direct revenue stream comes from the website, the indirect impact the website has is invaluable. Any adverse impact against the website's availability or integrity could mean a drastic loss in reputation for the organization. 

GoCD is critical to the success of the project, and continual success of this business function. GoCD is the System of Interest.

GoCD Server Specifications
*	Linux CentOS 7.3 Server
*	JDK 8 
*	Git (1.9+)
*	NodeJS 8
*	Python 2
*	yarn package manager
*	gcc/g++ 6

![System Engineering View of GoCD](https://github.com/SA-Java-CCSW/CYBR8420ProjectGoCD/blob/master/MisuseCases/SystemEngineeringView.png)


The organization has the following stakeholders that depend on the security of GoCD:

**Executive Management** are concerned with creating competitive advantage by using GoCD with it's DevOPs transformation. Security violations can damage the organization's profit margins and reputation.

**DevOPs Team** are concerned with the success of the project. Security violations can adversely impact the success of their project.

**Clients** are concerned about the image of their brand. Security violations can damage their reputation.

**Consumers** are trusting the website they visit will be secure and free of malicious code.

DevOPs Team members include the following:

**DevOps Evangelist** is the leader of the DevOPs transition project for the organization; seeking executive support and organizing DevOP software projects.

**Software Developer** are the programmers and developers producing the code.

**Security and Compliance Engineers** are responsible to meet security and compliance requirements for the project working in conjuction with DevOP developers.

**Release Manager** is responsible for coordinating development, testing, and deployment of the project.

**Automation Architect** is responsible for designing and creating GoCD pipelines for continuous delivery.

**QA Tester** responsible for creating automated and manual Jobs and Tasks for quality assurance purposes.

**Utility Technology Professionals** (or System Administrators) are responsible for setting up external systems; such as the git repositories and webserver. 


##### Data Flows
1. User Login & Management - *Example: GoCD System Administrator enables one or more chosen authentication methods and manages users with proper permissions via user/role based authorization*
2. User Creates Value Stream Map (VSM) - *Example: User creates end-to-end from commit to deployment workflow or the so-called Value Stream Map (VSM)*
3. Pipeline Locking: Run Instance of Pipeline - *The pipeline is not unlocked if it reaches a manual stage. If a pipeline is locked, it will not allow any new instances to run, unless it is unlocked, either manually or through the API.*
4. Trigger Pipeline Events - *Example: GoCD will trigger pipelines either automatically or manually depending on configuration settings when a material source is updated, such as a repository commit.*
5. Plugin Add/Delete/Configure: Add/Delete a plugin to GoCD server. Plugin is an extension to GoCD server which can help GoCD operation.*Example: Yum Repository Poller is installed to GoCD server, it helps polling yum repositories for rpm packages, and GoCD server interacts with this plugin via package material plugin interfaces.*

##### Threat Actor Examples
There are many threat actors that might want to attack an GoCD Server when it contains valuable software to be deployed.  Threat actors might also want to disrupt the functions that GoCD provides to the software development team.  The following are some examples of threat actors identified for this scenario.
1. External Attacker
2. Malicious Insider User
3. Hacktivist Agents

### Use Cases / Misuse Cases

##### Use Case 1
##### User Login & Management
![Malicous User Modifies VSM](https://github.com/SA-Java-CCSW/CYBR8420ProjectGoCD/blob/master/MisuseCases/UserManagement.png) 
A newly installed GoCD server does not require users to authenticate which is great for a test drive of GoCD. However, enabling authentication is one of the first things you should do, as soon as you decide to use GoCD more widely. GoCD provides many different authentication plugins. Two authentication plugins are bundled with GoCD installation. One is password file based authentication which allows you to create an encrypted username/password file saved on the GoCD Server via the plugin command line interface (CLI) or the htpasswd program from Apache Web Server package. It is highly recommended to force password hashing with bcrypt which is currently considered to be very secure. The other is the popular LDAP server based authentication. Besides these two bundled authentication plugins, GoCD also provides optional third-party authentication plugins such as Google OAuth or Github OAuth plugins which requires installation. One security issue with LDAP server and other OAuth third-party authentication is that by default GoCD allow users to automatically login via third-party plugin authentication into GoCD, even if these users haven't been explicitly added to GoCD. This is convenient for GoCD Admins to add new users, but should be disabled for security reasons explained later. Once authentication is enabled, the default is that any user can perform any operation. Specifying administrators(Admin) is optional – without it, all users are automatically made Admins(newly added users can be GoCD Admins). However, once a user is specified as GoCD Admin, other users will lose their Admin permissions unless they are specified as Admins as well. Only GoCD Admins are able to authorize users with different permissions via its role-based authorization. A role in GoCD is just a group of users which can be assigned with different permissions. Only GoCD Admins are able to create new pipeline groups and assign specified user or role as Pipeline Group Admins(PGA). PGA has permission to control which users/roles have view/operate/admin permissions for their assigned pipeline group. If GoCD Admin does not set any permission control on a newly created pipeline group, then any user is able to view/operate pipelines defined in that pipeline group. Only GoCD Admins are able to create new pipeline templates and assign specified user or role as Pipeline Template Admins(PTA). PTA has permission to create/modify stages in their assigned pipeline template. 

The misuse case mainly focused on blackmailing GoCD users for money by external attackers via DoS(Denial of Service) attack/getting unauthorized permissions/Unauthored logins. DoS attacks could threaten user's ability to login GoCD which could be prevented by implementing a feature to limit IP range/Add Duo Mobile authentication. Getting unauthorized permission could threaten the entire process of GoCD pipeline configuration which could be prevented by user/role-based authorization. Unauthorized auto-login could threaten every aspect of GoCD administration if an auto-login user is added as GoCD Admin, which can be prevented by disabling user login without existing accounts.

Security Requirements
* Role-based access control should be enabled to prevent users from getting unauthorized permissions on the entire configuring process of GoCD pipeline.
* Automatically login via third-party plugin authentication into GoCD should be disabled to prevent new users from becoming GoCD Admins automatically. 
* A feature to limit IP range/Add Duo Mobile authentication to the user Sign-in service should be implemented to prevent DoS attacks.

GoCD seems to have Role-based access control feature enabled. Role based access controls and security privileges are very clearly documented in their documentation [Role based access controls page](https://docs.gocd.org/current/configuration/dev_authorization.html). However, it should disable auto-login via third-party plugin authentication into GoCD by default. 

From my observation, GoCD failed in securing the user login service from DoS attacks and a feature to limit IP range/Add Duo Mobile authentication is highly recommended.

##### Use Case 2
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
##### User runs single/multiple instances of pipeline

![Pipeline Locking: Run Instance of Pipeline](https://github.com/SA-Java-CCSW/CYBR8420ProjectGoCD/blob/master/MisuseCases/RunPipelineInstance.png)

Sometimes user wants to make sure that there has only a single instance of a pipeline is running, in this case, make sure the stages of a pipeline are interrelated is very important. For the example, if the first stage may set up an environment, however, that environment is already used by the next stage in the pipeline, it will cause conflict between these two stages. Thus, GoCD come up with a solution. If a pipeline is locked, GoCD will not allow any other instance of that pipeline to be scheduled until the currently running one has been completed. When pipeline finishes, no matter it is end up with failure of any stage or success of the final stage, the pipeline is automatically unlocked to achieve the principle. However, pipeline could also be unlocked if reaches a manual stage, which means there is a window that allows malicious user who could reaches this stage and unlock the pipeline maliciously to make pipeline continue operate in the incorrect way. 

What's more, misuse case could also happen when developer wants to controll locking behavior from the config XML. To understand more detail about GoCD configuration reference, link below provide detail of [GoCD Configuration Reference](https://docs.gocd.org/current/configuration/configuration_reference.html#pipeline).

Security Requirements
* When instances in pipeline sometime need to ensure only one single instance of pipe line can run at a time, GoCD should remain the instances' consistency. 
* Make sure stages of pipeline are not related in aspects such as resources, because different stages require the same resource might cause "deadlock".

Based on what I have observed, the reason why lock or unlock pipelines is to prevent situation such as running multiple agents at the same time. However, if one of the stages fails, the pipeline is stop, thus it is unnecessary to ask developer to resume the pipeline manually. GoCD could automatically start over again after probelm is solved. However, for GoCD, if the stage is fails, the lock of pipeline is intentional. Because when pipeline fails at stage that caused by certain unprepared resources, there is no point for any other instance in pipeline to continue running. However, if pipeline lock cuased by deployment script, then another checkin is required and the pipeline should be resumed automatically. Thus, GoCD provides option to user to unlock pipeline if necessary. Pipeline in GoCD is in first class built-in concepts, pipeline is triggered as a unit. In order to prevent situation such as pipeline maliciously continue operating even fails occur, pipelines in GoCD are depending on another pipeline and artifacts flow through pipelines, each two instance between pipeline is compared and analyzed.

##### Use Case 4
#####  Trigger Pipeline Events
![Trigger Pipeline Events](https://github.com/SA-Java-CCSW/CYBR8420ProjectGoCD/blob/master/MisuseCases/TriggerPipelineEvents.png)

GoCD will automatically start the pipeline workflow when a repository commit is detected by GoCD's Material update sub-system(MCU). Once a change is detected, default GoCD behaviour will poll material components from the repository and begin triggering subsequent pipeline stages. A unauthorized commit performed by an external threat through a misconfigured repository can introduce malicious code into the software project. Human authorization can provide assurance that the risk introduced by misconfigured enabling systems is mitigated. This can be performed by having GoCD's administrator configure pipeline settings to only poll material components with manual user interaction. 

GoCD's role-based authorization is used to protect and insider threat to modify GoCD's pipeline configuration settings; namely, GoCD's material component repository settings. If role-based authorization is not configured correctly, a insider threat could configure material component source to a repository owned by a threat agent, and trigger a commit, introducing malicious code. Role-based authorization should be setup by the administrator to protect against this insider threat. 

Risks from external threats exist when GoCD polls material components from a repository over the network. First, GoCD requires in-transit encryption to protect against network easedropping and prevent unauthorized disclosure of information to an external threat. GoCD provides SSL/TSL encryption to protect material polling over the network and should be configured to protect against this threat. If an external threat is able to spoof a repository source to a repository containing malicious code, some form of integrity check should be provided to protect against a repository source spoofing attack. Finally, network validation should be implemented on GoCD's network interface to protect against network attacks, such as malformed network packets sent by an external threat to cause system crashes.

##### Use Case 5
#####  Add/Delete Plugin to GoCD Server
![Go Plugin add/delete/upgrade](https://github.com/SA-Java-CCSW/CYBR8420ProjectGoCD/blob/SReq_s/MisuseCases/GoPluginUseCase.png)
Plugins allow user to extend the functionalty of GoCD. Different kinds of plugins can be added to GoCD server. There are two types of plugins: Bundled plugins and External plugins. Bundled plugins are developed and supported by Thoughtworks GoCD development team. External plugins are all user authored plugins. GoCD server upgrade won't alter External plugins. Access to the GoCD server machine to be able to install/uninstall a plugin. To install a plugin, drop the plugin jar under the external plugin directory and restart GoCD server. To uninstall a plugin, remove the plugin jar from the external plugin directory on server and restart GoCD server. Plugins installed on GoCD server can also be upgraded. Admin users are allowed to check the plugin's status and failed reason. A malicious user might wants to change how the plugin runs in the GoCD server either by modify plugin identification id or fake authentification to request plugin information to GoCD server. A plugin metadata file should be used to maitain plugin unique id and admin user authentication methods mentioned in "User Login & Manangement" use case should help prevent it.

Security Requirements
* maintain uniqiue plugin id and metadata for plugin validation and security
* add/delete/modify plugin should take effect only when GoCD server is restarted
* an analysis utility should be avaliable so that users can commuicate with GoCD server about plugin status and settings.

From GoCD documentation, structure of a GoCD Plugin is a self contained plugin jar file. The jar file should contain plugin.xml (metadata of plugin), plugin extension class, and optional dependencies. Each plugin is assigned an identifier determined either by the id attribute in plugin metadata file or assigned as plugin jar file name. 

Plugin Tab is under GoCD Server Administration. It shows all currently loaded plugins with details and status. It also marks invalid/incompatible plugin and reports the reasons.
[GoCD Plugin User Guide](https://docs.gocd.org/current/extension_points/plugin_user_guide.html)
Available plugins in GoCD includes Yum Repository Poller, SCM externsion, Task externsion, etc. check [GoCD Plugins](https://www.gocd.org/plugins/) for available plugins. They are grouped into artifact plugins, authorization plugins, configuration repository, elastic agents plugins, notification plugins, package repository plugins, SCM plugins, Secrets plugins, Task plugins and Commecial Offerings.

Add/delete/upgrade of a plugin will take effect only after a GoCD server restarts.
Two plugins can't have same id. If two external plugins with same id are available, then only one of them will be loaded successfully with no specific order. If one external plugin and one bundled plugin has same id, then the bundled plugin will always be loaded.

An analytics extension point can be implemented when a plugin implements these four messages: Get Capabilities, Get Static Assets, Get Analytics, Plugin Settings Changed. To allow users to configure a plugin through the browsers, the plugin should implement thess four geneal purpose messages: Get Plugin Icon, Get Settings View, Get Plugin Configuration, Validate Plugin Configuration. Refer to [GoCD Plugin API](https://plugin-api.gocd.org/current/#introduction) for more information. Request to GoCD server can be sent as JSON object, and Response is also JSON object.

[GoCD Server Backup](https://docs.gocd.org/current/advanced_usage/one_click_backup.html) doesn't backup plugins. It backups Database, Configuration, XML Configuration Version Repo, GoCD version.


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
* Pipeline workflow stages can be set to be performed automatically or require human intervention to perform stages manually. GoCD is configured to trigger pipelines automatically when the Material update sub-system(MCU) detects a commit from a material source. Configuring pipelines to poll material components manually will mitigate unauthorized commits on enabling systems. 

#### TLS/SSL settings
* We can choose which ciphers and SSL/TLS protocols GoCD Server will use for communication with GoCD agents and users (and their browsers). We can configure system properties go.ssl.ciphers.include,	go.ssl.protocols.include etc. in  ${INSTALL_DIR_GO_SERVER}/wrapper-config/wrapper-properties.conf on GoCD Server and configure system property go.ssl.agent.protocol in ${INSTALL_DIR_GO_AGENT}/wrapper-config/wrapper-properties.conf on GoCD Agent. The default transport protocol that agent uses to communicate with Go server is TLSv1.2. 
* The GoCD server on first startup will create a self-signed SSL certificate that is ready for use by you. We may replace GoCD’s certificate with our own following [GoCD User Documentation](https://docs.gocd.org/current/installation/ssl_tls/custom_server_certificate.html).
* The agent by default trusts any and all certificates offered to it, which may possibly allow for MITM attacks. If we’d like to improve security further, by providing our own server certificate, we may add "wrapper.app.parameter.103=-rootCertFile", "wrapper.app.parameter.104=/path/to/root-cert.pem", "wrapper.app.parameter.105=-sslVerificationMode" and "wrapper.app.parameter.106=FULL" in ${INSTALL_DIR_GO_AGENT}/wrapper-config/wrapper-properties.conf before starting the GoCD agent process.

### Project Links
* Team Repository: https://github.com/SA-Java-CCSW/CYBR8420ProjectGoCD
* Project Board: https://github.com/SA-Java-CCSW/CYBR8420ProjectGoCD/projects/2
