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
                    bat 'docker build -t priyachitra/contactmanager .'
                }
            }
        }

        stage('Push Image to DockerHub') {
            steps {
                script {
                    withCredentials([string(credentialsId: 'chitra-dockerhub-sec', variable: 'dockerpwd')]) {
<<<<<<< HEAD
                        bat "docker login -u priyachitra -p ${dockerpwd}"
=======
                        bat "docker login -u priyachitra -p %dockerpwd%"
>>>>>>> branch 'main' of https://github.com/priyasri923/contactmanager_jenkins.git
                    }
<<<<<<< HEAD
                    bat 'docker push priychitra/contactmanager'
=======
                    bat 'docker push priyachitra/contactmanager'
>>>>>>> branch 'main' of https://github.com/priyasri923/contactmanager_jenkins.git
                }
            }
        }
    }
}
