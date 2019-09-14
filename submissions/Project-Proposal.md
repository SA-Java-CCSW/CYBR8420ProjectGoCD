## Project Proposal - GoCD
GoCD is a free, open-source continuous delivery server. The server is meant to be used by software development teams in Agile or DevOp environments. The project is sponsored and maintained by [ThoughtWorks](https://www.thoughtworks.com/), a software development consulting company.

GoCD will be referred to as "software" in this proposal.

The software will be used in a hypothetical software development environment at the enterprise level using the continuous integration methodology. The proposed project will involve software assurance analysis to be conducted on the software. Software assurance will identify potential security weaknesses that exist during the project's intended use, and provide justifiable confidence that the software will run correctly under adverse conditions under specific threat environments.


### Contributors
The software project community invites all to contribute toward the software's use and improvement.

The software's [Contributor Guide](https://www.gocd.org/contribute/) describes how to contribute to the project. 

There are various ways to contribute to the software project. Contributors can:
* Test run the project and report discovered [issues](https://github.com/gocd/gocd/issues). 
* Contribute code to the project by creating a [pull request](https://github.com/gocd/gocd/).
* Create a [plugin](https://docs.gocd.org/current/extension_points/plugin_user_guide.html) to extend the server's functionality.
* Research and [report](https://hackerone.com/gocd) any security issue found in GoCD
* Join [GoCD Forums](https://groups.google.com/forum/#!forum/go-cd) and discuss issues, features and ideas.
* Contribute to GoCD's [blog](https://www.gocd.org/blog/). 


![Contributors Per Month](https://github.com/SA-Java-CCSW/CYBR8420ProjectGoCD/blob/master/images/community.jpg)


### Activity
This project has nearly 9,930 commits by around 217 contributors and over a 696,809 lines of code. Statistics for this project are analyzed from the [GoCD on OpenHub](https://www.openhub.net/p/gocd).

![Commit Activity of GoCD](https://github.com/SA-Java-CCSW/CYBR8420ProjectGoCD/blob/master/images/activity.jpg)

![Lines of Code](https://github.com/SA-Java-CCSW/CYBR8420ProjectGoCD/blob/master/images/code.jpg)

The software is a well established, mature project. The software project began in December 2013 and has a large, active community.


### Popularity
38 companies reportedly use the software in their technology stacks according to https://stackshare.io/go-cd  

![Popularity of GoCD](https://github.com/SA-Java-CCSW/CYBR8420ProjectGoCD/blob/master/images/popularity.jpg)


### Languages Used
The language used to develop GoCD is Java. GoCD uses a dialect of Java called JRuby on Rails. Some parts of the server use Groovy, another dialect of Java. Other languages include HTML, XML, and CSS.  

![Languages Used](https://github.com/SA-Java-CCSW/CYBR8420ProjectGoCD/blob/master/images/language.jpg)


### Platform Used
For project developers, the technology stack is as follows:
* JDK 8 or above(OpenJDK or Oracle)
* Git (1.9+)
* NodeJS latest of 8.x (https://nodejs.org/en/download/)
* Python 2.x [Note: Python 3 does NOT work]
* yarn package manager (https://yarnpkg.com/en/docs/install)
* gcc/g++ 6.x (linux only). CentOS/RH users can find it here. Ubuntu 12.04 and 14.04 users can find it here.
* Microsoft Visual C++ Build Tools 2015 (Windows only).
* Microsoft Build Tools 2015 (Windows only).

Help setting up the environment can be found on GoCD's [Developer documentation](https://developer.gocd.org/current/2/2.1.html).

The application interface runs on browsers like Chrome. 

As a continuous delivery server, supporting systems such as a github repository and a deployment environment are required in order to use the software's intended functionality. 


### Documentation Sources
Main features and other detailed information is explained in [GoCD features page](https://www.gocd.org/why-gocd/). Main user documentation can be found on the [GoCD User Documentation](https://docs.gocd.org/current/) page. Other resources can be found at [GoCD Resources](https://www.gocd.org/resources/) page.


### License
GoCD is licensed under the [Apache License, version 2.0](https://www.apache.org/licenses/LICENSE-2.0). Our project adopts the same license.

Contributors that add or modify code to the project must first sign the [Contributor License Agreement(CLA) form](https://www.gocd.org/contributor-license-agreement/) before the code is implemented in the software project.


### Procedure for making contributions
GoCD is an open source project so anyone can contribute their code through the GitHub source. Anyone is encouraged to be contributors to the software. Contributors are highly encouraged to be involved in the community forum to organize contribution efforts.

To contribute code to the software project, the process is as follows:
1. Decide what you want to build through discussions on the community forum.
2. Fork the repository, keeping the repository in sync with the master.
3. Talk to the GoCD contributors over the GoCD Forums.
4. Make the changes to the GoCD project.
5. Submit a pull request.
6. Fill out the [Contributor License Agreement(CLA) form](https://www.gocd.org/contributor-license-agreement/).
7. The GoCD team will merge the request.

### Security History
The software project uses [hackerone](https://hackerone.com/gocd/) to track security vulnerabilities. As of date, there are 40 security reports that have been posted and resolved.

### User Security Needs
The software requires security features to safegaurd information flow and system functions from unauthorized modification and disclosure.

Two major threats to the software are:

**Insider Threats** such as developers inside the enterprise.

**Outsider Threats** such as cybercriminals outside the enterprise.

Some basic security features required to ensure security are:

**User authentication** to protect data flow from unauthorized modifications.
> *Scenario: An outsider threat is able to exploit authentication mechanism of the software and modify information flow.*

**Data Integrity** to prevent accidental data loss, corruption and unintentional modifications.
> *Scenario: An outsider threat is able to disrupt information flow between supporting systems and the software.*
    
**Identity Access Management** to ensure different role of users could appropriately access to corresponding resources.
> *Scenario: An insider threat does injects code into the build stream by accessing and modifying pipeline jobs through role permissions.*
    
**Access controls** on build chains.
> *Scenario: An insider threat modifies a pipeline that should not be changed.*
       
**Data Encryption** to protect data as it travels throughout build pipeline.
> *Scenario: SSL/TSL is not properly implemented by the software, allowing for disclosure of data that could allow a threat to gather information that could lead in a software breach.*

**Secure Configuration** to ensure build processes and automation remain secure.
> *Scenario: The software is configured to build upon repository pull request. An outsider threat can pull build and trigger the software to begin building malicious code.*

**Principle of Least Privileges** to make sure the software using micro-services and plugins are not compromised by trust relationships.
> *Scenario: Plugins give too much privileges by default allowing a threat to obtain elevated privileges on the system or software.*

        
### Security Features
The software has built-in encryption with SSL/TSL, authentication features, access tokens for api calls, user authorization settings, and group permissions. The software's security features are meant to protect and safeguard data flow from third-party ease-droppers and unauthorized modification. Some of the software's security features must first be configured to work correctly. Thus, depending on the enterprise's need  

### Motivations
The software is used for continuous integration in software development environments. Continuous integration is becoming more popular in Agile and DevOp teams as it allows for quicker development, testing and deployment of technology value streams. Continuous integration allows the code base to always be in a deployable state by merging all branches into a repository trunk through automation. Since Agile and DevOp methodologies focus on speed of deployment, security features within the software might be lacking against known threats to continuous integration.

New research is being conducted on continuous integration software; such as the [CIDER framework](https://github.com/spaceB0x/cider). New security frameworks might help assure security on the software project.

### Project Links
* Team Repository: https://github.com/SA-Java-CCSW/CYBR8420ProjectGoCD
* Project Board: https://github.com/SA-Java-CCSW/CYBR8420ProjectGoCD/projects

