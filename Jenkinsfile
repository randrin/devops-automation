pipeline {
    agent any
    tools{
        maven '3.9.5'
    }
    stages{
        stage("Build Maven") {
            steps{
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/randrin/devops-automation']])
                bat 'mvn clean install'
            }
        }
        stage("Build Docker image") {
            steps {
               script {
                    bat 'docker build -t randrino/devops-automation .'
                }
            }
        }
        stage("Push image to Docker Hub") {
            steps {
                script {
                    withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerhubpwd')]) {
                        bat 'docker login -u randrino -p Passaporto2003*'
                        bat 'docker push randrino/devops-automation'
                    }
                }
            }
        }
    }
}