pipeline {
    agent any

    tools {
        jdk 'JDK-17'
        maven 'Maven3'
    }

    stages {
        stage('Build Maven'){
                steps{
                    checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/priyasri923/contactmanager_jenkins.git']])
                    bat 'mvn clean install'
                }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    bat 'docker build -t priyachitra/contactmanager:2.0 .'
                }
            }
        }

        stage('Push Image to DockerHub') {
            steps {
                script {
                    withCredentials([string(credentialsId: 'chitra-dockerhub-sec', variable: 'dockerpwd')]) {
                        bat "docker login -u priyachitra -p ${dockerpwd}"
                    }
                    bat 'docker push priyachitra/contactmanager:1.0'

                }
            }
        }
        stage('Deploy to k8s'){
            steps{
                script{
                   withCredentials([file(credentialsId: 'kubeconfig-credentials', variable: 'KUBECONFIG')]) {
                    bat "kubectl apply -f deployment.yaml --kubeconfig=%KUBECONFIG%"
                    bat "kubectl apply -f service.yaml --kubeconfig=%KUBECONFIG%"
                    bat "kubectl rollout status deployment/contactmanager-deployment --kubeconfig=%KUBECONFIG%"
                }
                }
            }
        }
    }
}
