pipeline {
    agent any

    options {
        timestamps()
        disableConcurrentBuilds()
    }

    stages {
        stage('Install sam-cli) {
            steps {
                sh 'python3 -m venv venv && venv/bin/pip install aws-sam-cli'
                stash includes: '**/venv/**/*', name: 'venv'
            }
        }

        stage('Build') {
            steps {
                unstash 'venv'
                sh 'venv/bin/sam build'
                stash includes: '**/.aws-sam/**/*', name: 'aws-sam'
            }
        }

        stage('Test') {
            steps {
                echo 'this stage is to test'
            }
        }

        stage('Infrastructure Build') {
            steps {
                echo 'this stage is for infrastructure build'
            }
        }
        stage('Deployment to Staging Env') {
            steps {
                echo 'this stage is to deploy into staging'
            }
        }
        stage('Deployment to Production') {
            steps {
                echo 'this stage is for production deployment'
            }
        }


    }
}
