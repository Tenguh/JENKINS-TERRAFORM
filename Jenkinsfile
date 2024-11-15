#!/usr/bin/env groovy
pipeline{
    agent any
    tools {
        maven 'maven 3.6'
    }
    environment {
        IMAGE_NAME = 'tenguh/demo-app:java-maven-app-1.0'
    }
    stages {
        stage("build the app")
        steps {
            script {
                echo "building the application..."
                sh "mvn clean package"
            }
        }
        stage("build image")
        steps{
            script{
                echo "Building the docker image..."
                withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: 'PASS')]){
                    sh "docker build -t $IMAGE_NAME ."
                    sh "echo $PASS | docker login -u $USER --password-stdin"
                    sh "docker push  $IMAGE_NAME"
                }
                    

            }
        }

    }
        
}
        