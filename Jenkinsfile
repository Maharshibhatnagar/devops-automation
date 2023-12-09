pipeline {
    agent any
    tools{
        maven 'Maven3'
    }
    stages{
        stage('Build Maven'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Maharshibhatnagar/devops-automation']]])
                sh 'mvn clean install'
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t maharshibhatnagar/devops-integration .'
                }
            }
        }
        stage('Push image to DockerHub'){
            steps{
                script{
                   withCredentials([string(credentialsId: 'dockercred', variable: 'dockerhubpwd')]) {
                   sh 'docker login -u maharshibhatnagar -p ${dockerhubpwd}'

}
                   sh 'docker push maharshibhatnagar/devops-integration'
                }
            }
        }
         // stage('Deploy to k8s'){
         //     steps{
         //         script{
         //             kubernetesDeploy (configs: 'deploymentservice.yaml',kubeconfigId: 'k8sconfigpwd')
         //         }
         //     }
        // }
    }
}
