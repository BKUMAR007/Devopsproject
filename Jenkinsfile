pipeline {
    agent any
    stages {
        stage ('Check out step') {
            steps {
                 git url: "https://github.com/BKUMAR007/Devopsproject.git", branch: "dockerise"
                }
        }
         stage ('Maven build') {
            steps {
                sh "mvn clean package"
                }
        }
         stage ('Docker Build step') {
            steps {
                sh "docker build -t my-app ."
                }
        }
        stage ('Push to docker hub') {
            steps {
                withCredentials([usernamePassword(credentialsId:"DockerHubCreds",
                passwordVariable: "dockerHubPass",
                usernameVariable: "dockerHubUser"
                )]) {
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker image tag my-app ${env.dockerHubUser}/simple-java-app"
                sh "docker push ${env.dockerHubUser}/simple-java-app:latest"
                }
            }
        }
    }
}
