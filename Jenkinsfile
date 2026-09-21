pipeline {
    agent any

    triggers {
        // Poll GitHub every 2 minutes; a new commit starts the pipeline automatically.
        pollSCM('H/2 * * * *')
    }

    options {
        timestamps()
        buildDiscarder(logRotator(numToKeepStr: '10'))
    }

    stages {

        stage('Build') {
            steps {
                echo 'Stage 1 - Build'
                echo 'Task: compile the source code and package it into a deployable artefact (JAR/WAR).'
                echo 'Tool: Apache Maven (mvn clean package), with Nexus Repository as the artefact store.'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Stage 2 - Unit and Integration Tests'
                echo 'Task: run unit tests to verify each class behaves as expected, then run integration tests to verify the modules work together.'
                echo 'Tools: JUnit 5 with Mockito for unit tests, and REST Assured driven by Maven Failsafe for integration tests.'
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Stage 3 - Code Analysis'
                echo 'Task: perform static analysis of the code base against industry coding standards and report maintainability, reliability and duplication.'
                echo 'Tool: SonarQube Server via the Jenkins SonarQube Scanner plugin, with a quality gate applied to the build.'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Stage 4 - Security Scan'
                echo 'Task: scan the application and its third-party dependencies for known vulnerabilities (CVEs) and insecure code patterns.'
                echo 'Tools: OWASP Dependency-Check for the dependency CVE scan, and Snyk Code for static application security testing.'
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Stage 5 - Deploy to Staging'
                echo 'Task: deploy the packaged artefact to the staging server, which mirrors the production configuration.'
                echo 'Tools: AWS CLI to push the artefact to an Amazon EC2 staging instance, with Ansible playbooks performing the release.'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Stage 6 - Integration Tests on Staging'
                echo 'Task: run end-to-end and API integration tests against the staging deployment to confirm the application behaves correctly in a production-like environment.'
                echo 'Tools: Postman collections executed by Newman for the API tests, and Selenium WebDriver for the browser-based end-to-end tests.'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Stage 7 - Deploy to Production'
                echo 'Task: promote the verified release to the production environment using a controlled, repeatable deployment.'
                echo 'Tools: AWS CodeDeploy performing a blue/green release onto the production Amazon EC2 instances, with the infrastructure defined in Terraform.'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully: all seven stages passed.'
        }
        failure {
            echo 'Pipeline failed. Review the stage log above to identify the failing stage.'
        }
    }
}
