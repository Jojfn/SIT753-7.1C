# SIT753 Task 7.1C - Part 1, Task 1

Jenkins Continuous Integration pipeline integrated with GitHub.

**Unit:** SIT753 Professional Practice in IT
**Student:** Jason Hu (219220123)

The `Jenkinsfile` in this repository defines a seven-stage declarative pipeline. The Jenkins
job is configured as *Pipeline script from SCM* and polls this repository every two minutes
(`pollSCM('H/2 * * * *')`), so pushing a new commit starts a build automatically without a webhook.

| Stage | Task | Tool |
|-------|------|------|
| 1. Build | Compile and package the source into a deployable artefact | Apache Maven, Nexus Repository |
| 2. Unit and Integration Tests | Verify individual classes, then verify modules together | JUnit 5 + Mockito, REST Assured + Maven Failsafe |
| 3. Code Analysis | Static analysis against industry coding standards | SonarQube Server (Jenkins scanner plugin) |
| 4. Security Scan | Detect known CVEs and insecure code patterns | OWASP Dependency-Check, Snyk Code |
| 5. Deploy to Staging | Release the artefact to a production-like staging server | AWS CLI (Amazon EC2), Ansible |
| 6. Integration Tests on Staging | End-to-end and API tests against staging | Postman/Newman, Selenium WebDriver |
| 7. Deploy to Production | Promote the verified release to production | AWS CodeDeploy (blue/green), Terraform |

This is a mock pipeline: each stage prints the task it performs and the tool that would carry it out.

<!-- Trigger check: commit pushed at 2026-09-21 19:48:17 -->
