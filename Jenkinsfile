pipeline{
    agent any
        tools{
            jdk 'JDK 17'
            maven 'Maven 3'
        }
        stages{
            stage('Build Maven'){
                steps{
                    checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/AjushaLalasan/contactmanager_jenkins']])
                    bat 'mvn clean install'
                }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    bat 'docker build -t ajusha/contactmanager .'
                }
            }
        }
        stage('Push Image to DockerHub') {
            steps {
                script {
                    withCredentials([string(credentialsId: 'ajusha-dockerhub-sec', variable: 'dockerpwd')]) {
                        bat "docker login -u ajusha -p ${dockerpwd}"
                    }
                    bat 'docker push ajusha/contactmanager'
                }
            }
        }
    }
}
