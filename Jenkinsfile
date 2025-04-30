pipeline {
    agent any   // Make sure this is correctly placed here
    
   environment {
        DOCKER_IMAGE = "clara100/abcapp"
        WORK_DIR = "/var/lib/jenkins/workspace/ci-cd"
    }

    stages {
        stage('Code Checkout') {
            steps {
                // Checkout code
                git url: 'https://github.com/cekwe/CI-CD-Project.git', branch: 'main'
            }
        }

        stage('Code Compile') {
            steps {
                // Compile the code using Maven
                sh 'mvn compile'
            }
        }

        stage('Test') {
            steps {
                // Run tests using Maven
                sh 'mvn test'
            }
        }

        stage('Build') {
            steps {
                // Package the application using Maven
                sh 'mvn package'
            }
        }
        stage('Build Docker Image') {
            steps {
                // Copy the WAR file and build the Docker image
                sh 'cp ${WORK_DIR}/target/ABCtechnologies-1.0.war abc_tech.war'
                sh 'docker build -t ${DOCKER_IMAGE}:latest .'
            }
        }

        stage('Push Docker Image') {
            steps {
                // Push Docker image to DockerHub
                withDockerRegistry([credentialsId: "docker-id", url: ""]) {
                    sh 'docker push ${DOCKER_IMAGE}:latest'
                }
            }
        }

        stage('Deploy as container') {
            steps {
                // Deploy the Docker container locally
                sh 'docker run -itd -p 8081:8081 --name abcapp1 ${DOCKER_IMAGE}:latest'
            }
        }
    }
}
