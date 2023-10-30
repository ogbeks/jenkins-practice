#!/usr/bin/env groovy

pipeline {
        agent any 
        stages {
            stage('Build Docker Image') {
                steps {
                    script {
                        docker.build("node-alpine:latest")
                    }
                }
            }
            stage('Push Docker Image') {
                steps {
                    script {
                        withCredentials([usernamePassword(credentialsId: 'DockerHubCreds', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                            sh "docker login -u ${USERNAME} -p ${PASSWORD}"
                            sh "docker push node-alpine:latest"
                        }
                    }
                }

        }
    }

