pipeline {
    agent any
    
    tools {
        jdk 'JDK17'
        maven 'M3'
    }
    
    stages {
        stage('Git clone') {
            steps {
                echo 'Git clone'
                git url: 'https://github.com/ezuyan/spring-petclinic.git',
                branch: 'efficient-webjars'
            }
            post {
                success {
                    echo 'Success git clone step'
                }
                failure {
                    echo 'Fail git clone step'
                }
            }
        }
        stage('Maven Build') {
            steps {
                echo 'Maven Build'
                sh 'mvn -Dmaven.test.failure.ignore=true install'
            }
            post {
                success {
                    junit '**/target/surefire-reports/TEST-*.xml'
                }
            }
        }
        stage('Docker Image Build') {
            steps {
                echo 'Docker Image build'
                dir("${env.WORKSPACE}") {
                    sh """
                        docker build -t ezuyan/spring-petclinic:$BUILD_NUMBER .
                        docker tag ezuyan/spring-petclinic:$BUILD_NUMBER ezuayn/spring-petclinc:latest
                    """
                }
                
            }
        }
        
        
        
        stage('Docker Image Upload') {
            steps {
                echo 'Docker Image Upload'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploy'
            }
        }
    }
}
