## Designing for Software Security Engineering
#### Data Flow 1: User Login & Management
Level 0 DFD

![Level 0 for User Login & Management](https://github.com/SA-Java-CCSW/CYBR8420ProjectGoCD/blob/master/Threat%20Models/UserLoginDFDLevel0.PNG)

The complete threat report along with Level 1 diagram for User Login & Management can be found <a href = "https://sa-java-ccsw.github.io/CYBR8420ProjectGoCD/Threat%20Models/UserLoginDFDLevel1-2.htm">here.</a>

#### Data Flow 2: User Creates Value Stream Map
Level 0 DFD

![Level 0 for User Login & Management](https://github.com/SA-Java-CCSW/CYBR8420ProjectGoCD/blob/master/Threat%20Models/UserCreatesVSMDFDLevel0-2.PNG)

The complete threat report along with Level 1 diagram for User Creates Value Stream Map can be found <a href = "https://sa-java-ccsw.github.io/CYBR8420ProjectGoCD/Threat%20Models/UserCreatesVSMDFDLevel1-2.htm">here.</a>

#### Data Flow 3: GoCD Backup
Level 0 DFD  

![Level 0 for GoCD Backup](https://github.com/SA-Java-CCSW/CYBR8420ProjectGoCD/blob/master/Threat%20Models/DataFlow3Level0ScreenShot.PNG)

The complete threat report along with Level 1 diagram for GoCD Backup can be found <a href = "https://sa-java-ccsw.github.io/CYBR8420ProjectGoCD/Threat%20Models/DataFlow3DFDReport.htm">here.</a>

#### Data Flow 4: Polling Material Components
Level 0 DFD

![Level 0 for Polling Material Components](https://github.com/SA-Java-CCSW/CYBR8420ProjectGoCD/blob/master/Threat%20Models/PollMaterialDFDLevel0.PNG)

The complete threat report along with Level 4 diagram for User Login & Management can be found <a href = "https://sa-java-ccsw.github.io/CYBR8420ProjectGoCD/Threat%20Models/PollMaterialDFDLevel1.htm">here.</a>

#### Data Flow 5: Plugin Extension Point Process
Level 0 DFD

![Level 0 for Plugin Extension Point Process](https://github.com/SA-Java-CCSW/CYBR8420ProjectGoCD/blob/master/Threat%20Models/Plugin_DFD5_L0.png)

The complete threat report along with Level 1 diagram for Plugin Extension Point Process can be found <a href = "https://sa-java-ccsw.github.io/CYBR8420ProjectGoCD/Threat%20Models/Plugin_DFD5_L1.htm">here.</a>

**Threat Model Analysis**  
GoCD has various ways to authenticate identity of users which makes spoofing users attack very unlikely. Role based access control and the default behavior of running go-server daemon as standard user "go" reduces the risk of elevation of privilege. GoCD has many additional features to be customized for logging detailed activities (See https://docs.gocd.org/current/advanced_usage/logging.html ) which help prevent repudiation threats in several analyzed data flows.

However, our threats model analysis does show some security issues which have not been mitigated by current implementation of GoCD. For example, GoCD lacks of ACL(Access Control List) such as IP restriction to protect its server from DoS Attack. GoCD lacks of a security feature to prove that users are actually login the authenticated legitimate website. May consider using third-party verified digital certificates or use user chosen login picture to identify the site itself. Some of these findings are consistent with our previous misuse case analysis from GoCD's security requirements.

### Project Links
* Team Repository: https://github.com/SA-Java-CCSW/CYBR8420ProjectGoCD
* Project Board: https://github.com/SA-Java-CCSW/CYBR8420ProjectGoCD/projects/4
