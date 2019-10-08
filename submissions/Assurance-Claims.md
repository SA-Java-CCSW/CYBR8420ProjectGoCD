## Assurance Claim - 1: 
**Top Claim 1:**

## Assurance Claim - 2: 
**Top Claim 2:**

## Assurance Claim - 3: 
**Top Claim 3:**

## Assurance Claim - 4: 
**Top Claim 4:**

![Preventions of unauthorized access](https://github.com/SA-Java-CCSW/CYBR8420ProjectGoCD/blob/AssuranceClaim4/AssuranceClaims/Assurance_Claim_4.png)

* **Evidence E.1.1.1:** When GoCD run out of disk space, GoCD notices user with warning box or error message to indicate the server has [run out of disk space](https://docs.gocd.org/current/faq/admin_out_of_disk_space.html), and the schedul has been stopped. GoCD could automatically delete the unused artifacts that occupied space on server. GoCD could also preserve artifacts that are important to the stage by disable deletion of specific artifact from the deleted process.

* **Evidence E.1.2:** By [default](https://docs.gocd.org/current/advanced_usage/dev_clean_up_when_cancel.html), GoCD kills current running tasks and clean up environment for jobs if user already know the jobs are going to fail.  

* **Evidence E.1.3:** To maintain the state inconsistent, GoCD can be indicated to finish certain task during the cleanup process. GoCD allows user to use web interface or XML configuration to perform the [custom cleanup](https://docs.gocd.org/current/advanced_usage/dev_clean_up_when_cancel.html).

## Assurance Claim - 5: 
**Top Claim 5:**

### Project Links
* Team Repository: https://github.com/SA-Java-CCSW/CYBR8420ProjectGoCD
* Project Board: https://github.com/SA-Java-CCSW/CYBR8420ProjectGoCD/projects/3
