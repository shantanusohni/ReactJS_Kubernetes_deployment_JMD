pipeline {
    agent any
    environment {
        PROJECT_ID = 'fresh-shell-275710'
        CLUSTER_NAME = 'jaimatadi'
        LOCATION = 'us-central1-a'
        CREDENTIALS_ID = 'gke'
    }
    stages {
        stage("Checkout code") {
            steps {
                checkout scm
            }
        }
        stage("Build image") {
            steps {
                script {
                    myapp = docker.build("shantanusohni/reactjs:${env.BUILD_ID}")
                }
            }
        }
        stage("Push image") {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                            myapp.push("latest")
                            myapp.push("${env.BUILD_ID}")
                    }
                }
            }
        }        
        stage('Deploy to GKE Cluster') {
            steps{
                sh "sed -i 's/reactjs:latest/reactjs:${env.BUILD_ID}/g' deployment.yaml"
            }
        }
    }    
}
