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
![Malicous User Modifies VSM](https://github.com/SA-Java-CCSW/CYBR8420ProjectGoCD/blob/master/MisuseCases/UserCreatesVSM.png)
GoCD is a best-of-breed tool for Continuous Delivery (CD) which allows a software development team to get changes of all types—including new features, configuration changes, bug fixes and experiments—into production, or into the hands of customers as quickly as possible. The most important use case in GoCD is to let users create an end-to-end from commit to deployment workflow or the so-called Value Stream Map (VSM). VSM helps you visualize your entire CI/CD workflow and allows you to trace a commit from when it is checked in up to when it is deployed. VSM is laid out as an end-to-end dependency graph originating from source control materials and flows from left to right passing various pipelines. Check [GoCD User Documentation](https://docs.gocd.org/current/navigation/value_stream_map.html) for more info. A GoCD pipeline consists of one or more "stages", each stage consists of one or more "jobs" and each job is made up of one or more "tasks". Each stage must run sequentially, but multiple jobs in the same stage are independent of each other and can be run in parallel at the same time. Each task in a job must run sequentially as well. Check [GoCD Get Started Tutorial](https://www.gocd.org/getting-started/part-1/#concept4) for more info about these key concepts in GoCD.

The misuse case mainly focused on configuring tasks of GoCD jobs in the GoCD pipelines by unauthorized internal Malicious user. Different operations can be performed to inject malicious codes into final deployed product. GoCD has implemented the protection mechanism for the role-based user access. Ways to control what data users can have access to and what tasks they can perform based on the security privileges are clearly documented in the [GoCD User Documentation](https://docs.gocd.org/current/configuration/dev_authorization.html)

Security Requirements
* Role-based access control should be enabled to prevent users from performing unauthorized actions on configuring the entire VSM workflow.
* Enable the IP filtering feature to prevent blacklisted IP’s from joining the GoCD Server. For example, the external attacker attempting to join the GoCD Server without permissions.

GoCD seems to have Role-based access control feature. Role based access controls and security privileges are very clearly documented in their documentation [Role based access controls page](https://docs.gocd.org/current/configuration/dev_authorization.html). 

From my observation, GoCD failed in securing the file-based user login data which is stored in the GoCD Server from the Ransomware attack. A feature of IP filtering through which only whitelisted ones only can access and perform certain operations on GoCD Server should be added. In addition, Duo Mobile authentication is highly recommended to improve its user login security.


##### Use Case 3
##### User runs single/multiple instances of pipeline

![Pipeline Locking: Run Instance of Pipeline](https://github.com/SA-Java-CCSW/CYBR8420ProjectGoCD/blob/master/MisuseCases/RunPipelineInstance.png)

Sometimes user wants to make sure that there has only a single instance of a pipeline is running. It is very important that the stages of a pipeline are interrelated. Here is the example, if the first stage may set up an environment, however, that environment is already used by the next stage in the pipeline. Thus, GoCD come up with a solution. If a pipeline is locked, GoCD will not allow any other instance of that pipeline to be scheduled until the currently running one has been completed. When pipeline finishes, no matter it is end up with failure of any stage or success of the final stage, the pipeline is automatically unlocked to achieve the principle. However, pipeline could also be unlocked if reaches a manual stage, which means there is a window that allows malicious agent who reaches this stage and unlock the pipeline maliciously to make pipeline continue operate in the incorrect way. 

What's more, misuse case could also happen when developer wants to controll locking behavior from the config XML. To understand more detail about GoCD configuration reference, link below provide detail of [GoCD Configuration Reference](https://docs.gocd.org/current/configuration/configuration_reference.html#pipeline).

Security Requirements
* When instances in pipeline sometime need to ensure only one single instance of pipe line can run at a time, GoCD should remain the instances' consistency. 
* Make sure stages of pipeline are not related in aspects such as resources, because different stages require the same resource might cause "deadlock".

I assumed the reason for the option to lock a pipeline is to prevent it from running on multiple agents concurrently. But if a stage fails, the pipeline is over, seems it is not necessary to ask developer to resume manually, it could just show message and automatically start over again after bug fixed. Pipeline staying locked even if the stage fails was intentional. Consider a deployment pipeline. If the pipeline fails at a stage then it could be due to some environment issues which needs to be sorted before the stage could proceed and there is no point for another instance to start running. But if the issue is with deployment script then another checkin is needed and the pipeline should get triggered even if some stage had failed. So essentially user should have an option to unlock it if needed. Exact approach yet to be decided.

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
