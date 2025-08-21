pipeline {
    agent any

    stages {
        stage('Hello1') {
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
                        sh(script: 'aws s3 cp /var/lib/jenkins/workspace/JenkinsPipline/index.html s3://test-jenkins-20250820/')
                }
            }
        }
        stage('Test') {
            steps {
                echo 'Test'
                script {
                    def url = 'https://test-jenkins-20250820.s3.ap-northeast-1.amazonaws.com/index.html'
                    def response = sh(script: "curl -s -o /dev/null -w '%{http_code}' '$url'", returnStdout: true)

                    if (response == '200') {
                        echo 'Test OK'
                    } else {
                        echo response
                        error 'Test NG'
                    }
                }
            }
        }
        stage('releas') {
            steps {
                echo 'releas'
            }
        }
    }
}
