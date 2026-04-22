6# 🚀 Jenkins Declarative Pipeline (QA Automation)

This document describes a complete Jenkins Declarative Pipeline for running a Python + Pytest automation framework.

---

## 📌 Pipeline Overview

Trigger → Checkout → Setup → Install → Test → Report → Notify

---

## ⚙️ Jenkins Pipeline Script

```groovy
pipeline {
    agent any

    parameters {
        string(name: 'ENV', defaultValue: 'dev', description: 'Environment')
        booleanParam(name: 'RUN_TESTS', defaultValue: true, description: 'Run tests or not')
        choice(name: 'BROWSER', choices: ['chrome', 'firefox'], description: 'Browser')
        string(name: 'MARKER', defaultValue: 'smoke', description: 'Pytest marker')
    }

    triggers {
        githubPush()
        cron('H 2 * * *')
    }

    stages {

        stage('Checkout Code') {
            steps {
                git 'https://github.com/your-repo.git'
            }
        }

        stage('Setup Virtual Environment') {
            steps {
                sh 'python -m venv venv'
                sh '. venv/bin/activate'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'pip install -r requirements.txt'
            }
        }

        stage('Run Tests') {
            when {
                expression { params.RUN_TESTS == true }
            }
            steps {
                script {
                    def result = sh(
                        script: "pytest -m ${params.MARKER} --env=${params.ENV} --alluredir=allure-results",
                        returnStatus: true
                    )

                    if (result != 0) {
                        currentBuild.result = 'FAILURE'
                        error("Tests failed")
                    }
                }
            }
        }

        stage('Generate Report') {
            steps {
                sh 'allure generate allure-results -o allure-report --clean'
            }
        }
    }

    post {

        success {
            mail to: 'team@example.com',
                 subject: "SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: "All tests passed successfully."

            slackSend (
                channel: '#qa-alerts',
                color: 'good',
                message: "Build Passed: ${env.JOB_NAME} #${env.BUILD_NUMBER}"
            )
        }

        failure {
            mail to: 'team@example.com',
                 subject: "FAILURE: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: "Tests failed. Check Jenkins logs."

            slackSend (
                channel: '#qa-alerts',
                color: 'danger',
                message: "Build Failed: ${env.JOB_NAME} #${env.BUILD_NUMBER}"
            )
        }

        always {
            archiveArtifacts artifacts: 'allure-report/**', fingerprint: true
        }
    }
}
```
