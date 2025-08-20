pipeline {
    agent any

    stages {
        stage('Hello') {
            steps {
                echo 'Hello from github webhook'
            }
        }
        stage('Build') {
            steps {
                echo 'Building'
            }
        }
        stage('deploy') {
            steps {
                echo 'deploy'
                withCredentials([[
                    $class: 'AmazonWebServicesCredentialsBinding',
                    credentialsId: 'MyAWS',
                    accessKeyVariable: 'AWS_ACCESS_KEY_ID',
                    secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]){
                        sh(script: 'aws s3 cp /var/lib/jenkins/workspace/JenkinsPipline/index.html S3://test-jenkins-20250820')
                }
            }
        }
        stage('Test') {
            steps {
                echo 'Test'
            }
        }
        stage('releas') {
            steps {
                echo 'releas'
            }
        }
    }
}
