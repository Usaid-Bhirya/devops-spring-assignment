pipeline {
    agent any
    tools {
        maven "Maven.v1"
    }
    
    stages {
        stage('Build Maven') {
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Usaid-Bhirya/devops-spring-assignment']])
                sh 'mvn clean install'
            }
        }
        
        stage('Build docker image') {
            steps {
                scripts {
                    sh 'docker build -t usaidbhirya/devops-integration .'
                }
            }
        }
        // stage('Push image to Hub'){
        //     steps{
        //         script{
        //            withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerhubpwd')]) {
        //            sh 'docker login -u javatechie -p ${dockerhubpwd}'}
        //            sh 'docker push javatechie/devops-integration'
        //         }
        //     }
        // }
        // stage('Deploy to k8s'){
        //     steps{
        //         script{
        //             kubernetesDeploy (configs: 'deploymentservice.yaml',kubeconfigId: 'k8sconfigpwd')
        //         }
        //     }
        // }
    }
}