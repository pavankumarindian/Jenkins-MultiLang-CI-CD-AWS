pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build and Test Maven') {
            steps {
                dir('maven-project') {
                    sh 'mvn clean install'
                }
            }
        }

        stage('Build Docker Image - Maven') {
            steps {
                script {
                    def imageName = 'your-docker-image-name-maven'
                    docker.build(imageName, '-f Dockerfiles/Dockerfile.maven .')
                }
            }
        }

        stage('Docker Compose - Maven') {
            steps {
                script {
                    sh 'docker-compose -f docker-compose-maven.yml up -d'
                }
            }
        }

        // Similar stages for Gradle, Python, and MS Build

        stage('Build Docker Image - Gradle') {
            steps {
                script {
                    def imageName = 'your-docker-image-name-gradle'
                    docker.build(imageName, '-f Dockerfiles/Dockerfile.gradle .')
                }
            }
        }

        stage('Docker Compose - Gradle') {
            steps {
                script {
                    sh 'docker-compose -f docker-compose-gradle.yml up -d'
                }
            }
        }

        stage('Build Docker Image - Python') {
            steps {
                script {
                    def imageName = 'your-docker-image-name-python'
                    docker.build(imageName, '-f Dockerfiles/Dockerfile.python .')
                }
            }
        }

        stage('Docker Compose - Python') {
            steps {
                script {
                    sh 'docker-compose -f docker-compose-python.yml up -d'
                }
            }
        }

        stage('Build Docker Image - MS Build') {
            steps {
                script {
                    def imageName = 'your-docker-image-name-msbuild'
                    docker.build(imageName, '-f Dockerfiles/Dockerfile.msbuild .')
                }
            }
        }

        stage('Docker Compose - MS Build') {
            steps {
                script {
                    sh 'docker-compose -f docker-compose-msbuild.yml up -d'
                }
            }
        }
    }
}
