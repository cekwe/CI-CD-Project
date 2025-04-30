pipeline {
    agent any   // Make sure this is correctly placed here
    


    stages {
        stage('Code Checkout') {
            steps {
                // Checkout code
                git url: 'https://github.com/cekwe/CI-CD-Project.git' branch: 'main'
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
    }
}
