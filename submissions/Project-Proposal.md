## Project Proposal - GoCD
GoCD is a free, open-source continuous delivery server. The server is meant to be used by software development teams in Agile or DevOp environments. The project is sponsored and maintained by [ThoughtWorks](https://www.thoughtworks.com/), a software development consulting company.

GoCD will be referred to as "software" in this proposal. 

The software will be used in a hypothetical software development environment at the enterprise level using the continuous integration methodology. 


### Contributors
The software's [Contributor Guide](https://www.gocd.org/contribute/) describes how to contribute to the project. 

There are various ways to contribute to the software project. Contributors can:
*Test run the project and report discovered [issues](https://github.com/gocd/gocd/issues). 
*Contribute code to the project by creating a [pull request] (https://github.com/gocd/gocd/).
*Create a [plugin](https://docs.gocd.org/current/extension_points/plugin_user_guide.html) to extend the server's functionality.
*Research and [report](https://hackerone.com/gocd) any security issue found in GoCD
*Join [GoCD Forums](https://groups.google.com/forum/#!forum/go-cd) and discuss issues, features and ideas.
*Contribute to GoCD's [blog](https://www.gocd.org/blog/). 

![Contributors Per Month](https://github.com/SA-Java-CCSW/CYBR8420ProjectGoCD/blob/master/images/community.jpg)


### Activity
This project has nearly 9,930 commits by around 217 contributors and over a 696,809 lines of code. Statistics for this project are analyzed from the [GoCD on OpenHub](https://www.openhub.net/p/gocd).

![Commit Activity of GoCD](https://github.com/SA-Java-CCSW/CYBR8420ProjectGoCD/blob/master/images/activity.jpg)

![Lines of Code](https://github.com/SA-Java-CCSW/CYBR8420ProjectGoCD/blob/master/images/code.jpg)

The software is a well established, mature project. The software project began in December 2013 and has an active community.


### Popularity
38 companies reportedly use GoCD in their technology stacks according to https://stackshare.io/go-cd  
![Popularity of GoCD](https://github.com/SA-Java-CCSW/CYBR8420ProjectGoCD/blob/master/images/popularity.jpg)


### Languages Used
The language used to develop GoCD is Java. GoCD uses a dialect of Java called JRuby on Rails. Some parts of the server use Groovy, another dialect of Java, HTML, XML, and CSS.  
![Languages Used](https://github.com/SA-Java-CCSW/CYBR8420ProjectGoCD/blob/master/images/language.jpg)


### Platform Used
For project developers, the technology stack is as follows:
*JDK 8 or above(OpenJDK or Oracle)
*Git (1.9+)
*NodeJS latest of 8.x (https://nodejs.org/en/download/)
*Python 2.x [Note: Python 3 does NOT work]
*yarn package manager (https://yarnpkg.com/en/docs/install)
*gcc/g++ 6.x (linux only). CentOS/RH users can find it here. Ubuntu 12.04 and 14.04 users can find it here.
*Microsoft Visual C++ Build Tools 2015 (Windows only).
*Microsoft Build Tools 2015 (Windows only).

Help setting up the environment can be found on GoCD's [documentation](https://developer.gocd.org/current/2/2.1.html).

For users, this application runs on browsers like Chrome. As a continuous delivery server, repository such as github and a deployment environment will be required.


### Documentation Sources
Main features and other detailed information is explained in [GoCD features page](https://www.gocd.org/why-gocd/). 


### License
GoCD is licensed under the [Apache License, version 2.0](https://www.apache.org/licenses/LICENSE-2.0). Our project adopts the same license.


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


### User Security Needs
Below are some basic security needs that users would probably need from the software package and are a couple of scenarios to highlight how it might exist in many different types of environments.

**User authentication** to protect data flow from unauthorized users and modifications.

**Data Integrity** to prevent accidental data loss, corruption and unintentional modifications.
    
**Identity Access Management** to ensure different role of users could appropriately access to corresponding resources.
> *Scenario: Ensure that an insider threat does not inject code into the build stream by accessing and modifying pipeline jobs through role permissions.*
    
**Access controls** on stored data procedures. 
       
**Data Encryption** to protect data as it travels throughout build pipeline.

**Secure Configuration** to ensure build processes and automation remain secure.
> *Scenario: GoCD is configured to build upon repository pull request. A malicious attacker can pull build and trigger GoCD to begin building malicious code.*
        
### Security Features


### Motivations
The software is used for continuous integration in software development environments. Continuous integration is becoming more popular in Agile and DevOp teams as it allows for quicker development, testing and deployment of technology value streams. Continuous integration allows the code base to always be in a deployable state by merging all branches into a repository trunk through automation. Since the 

### Project Links
* Team Repository: https://github.com/SA-Java-CCSW/CYBR8420ProjectGoCD
* Project Board: https://github.com/SA-Java-CCSW/CYBR8420ProjectGoCD/projects

