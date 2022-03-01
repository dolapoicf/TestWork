pipeline {
    agent any

    options {
        timestamps()
        disableConcurrentBuilds()
    }

    stages {
        stage('Install sam-cli') {
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

        stage('Beta') {
            environment {
                STACK_NAME = 'jenkins1-gao'
                S3_BUCKET = 'sam-jenkins-demo-goa-hhs'
            }
                steps {
                    withAWS(credentials: 'Jenkins_GAO, region: 'us-west-1) {
                        unstash 'venv'
                        unstash 'aws-sam'
                        sh 'venv/bin/sam deploy --stack-name $STACK_NAME -t template.yaml --s3-bucket $S3_BUCKET --capabilities CAPABILITY_IAM'
                        dir ('hello-world') {
                            sh 'npm ci'
                            sh 'npm run integ-test'                            
                        }
                    }
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
