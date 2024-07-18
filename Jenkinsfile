pipeline {
    agent any

    tools {
        dockerTool 'docker'
    }

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-credentials-id')
    }

    /* stages {

        stage('Build Backend') {
            steps {
                script {
                    // Build the backend Docker image
                    def backendImage = docker.build("got-backend", "./backend")
                }
            }
        }
         stage('Build Frontend') {
            steps {
                script {
                    // Build the frontend Docker image
                    def frontendImage = docker.build("got-frontend", "./frontend")
                }
            }
        }
        stage('Push to DockerHub') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', DOCKERHUB_CREDENTIALS) {
                        backendImage.push()
                        frontendImage.push()
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    sh 'docker-compose up -d'
                }
            }
        }
    }

        post {
        always {
            cleanWs()
        }
    } */
     
     


    stages {

        stage('Build Backend') {
            steps {
                script {
                    dir('backend') {
                        sh 'docker build -t got-backend .'
                        sh 'docker tag got-backend slimjemaidocker/got-backend:latest'
                    }
                }
            }
        }

        stage('Build Frontend') {
            steps {
                script {
                    dir('frontend') {
                        sh 'docker build -t got-frontend .'
                        sh 'docker tag got-frontend slimjemaidocker/got-frontend:latest'
                    }
                }
            }
        }

        stage('Push to DockerHub') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerhub-credentials-id') {
                        sh 'docker push slimjemaidocker/got-backend:latest'
                        sh 'docker push slimjemaidocker/got-frontend:latest'
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    sh 'docker-compose up -d'
                }
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    } 
}
