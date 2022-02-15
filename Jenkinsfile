pipeline {
    agent any

    options {
        timestamps()
        disableConcurrentBuilds()
    }

    stages {
        stage('intialize') {
            steps {
                echo 'this is to intialize the build'
            }
        }

        stage('Build') {
            steps {
                echo 'this stage is the build stage'
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
