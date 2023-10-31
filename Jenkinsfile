#!/usr/bin/env groovy

pipeline {
    agent any

    stages {
        stage('Build Docker Image') {
            steps {
                // git credentialsId: 'github-login', url: 'https://github.com/ogbeks/jenkins-practice.git'
                // sh "ls"
                script {
                    dockerImage = docker.build('node:12')
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
