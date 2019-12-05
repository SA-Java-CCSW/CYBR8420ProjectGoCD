1. Investigate login/authentication components against DoS/Spoofing attacks and if they support IP range based ACL(Access Control List) and user account lock out after N unsuccessful login attempts.

2. Investigate source materials validation components against Elevation Of Privilege/Tampering/Spoofing attacks

3. Investigate backup/restore components against Tampering/Repudiation attacks

4. Investigate poll material source components against Repudiation/DoS/Elevation Of Privilege attacks and if the setting that requires human intervention is enabled by default or not.

5. Investigate pipeline workflow components against Elevation Of Privilege attack and if they log pipeline setting changes. 

6. Investigate web ui component against DoS attack

7. Investigate material update sub-system(MCU) component against DoS attack

8. Investigate pluign extension point component against Elevation Of Privilege attack and if it has built-in advanced plugin validation mechanism such as checking integrity of plugin jar file: plugin.xml (metadata of plugin), plugin extension class, and optional dependencies.

9. Investigate authorization component to check if a new user is given the lowest privilege rights.

10. Investigate SSL/TLS component to check if a warning message or alert occurs if a insecure self-signed SSL certificate is being used.

11. Investigate authentication configuration component against Cross-Site Forgery Requests (CSFR) attack and if system property go.sessioncookie.maxage.seconds's default value.

12. Investigate usage of JRuby on Rails framework in GoCD to check if GET requests have anti-CSRF applied by default.
