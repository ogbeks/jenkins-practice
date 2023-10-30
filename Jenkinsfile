#!/usr/bin/env groovy

pipeline {
    agent any 

    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build('node-alpine')
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'DockerHubCreds', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                        docker.withRegistry('https://hub.docker.com/', "${USERNAME}:${PASSWORD}") {
                            dockerImage.push()
                        }
                    }
                }
            }
        }
    }
}
