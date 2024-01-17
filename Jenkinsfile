pipeline {
    agent any

    environment {
        M2_HOME = '/opt/apache-maven-3.2.5'
        PATH = "${M2_HOME}/bin:${PATH}"
    }

    tools {
        // Use 'maven' instead of 'Maven-3.2.5'
        maven 'maven'
    }

    stages {
        stage('Build') {
            steps {
                script {
                    // Use the 'dir' step to change directory
                    dir('workspace') {
                        // Clean and clone in the workspace directory
                        sh 'rm -rf aitouristguide-backend'
                        sh 'git clone https://github.com/snahammed506/aitouristguide-backend.git'
                        sh 'cd aitouristguide-backend'
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    // Use a loop for repetitive steps to avoid duplication
                    def services = ['feedback-service', 'admin-service', 'place-service', 'server-registery', 'tourplan-service', 'UserService']

                    services.each { service ->
                        dir(service) {
                            // Clean, build, and push Docker images
                            sh "mvn clean install -DskipTests && docker build -t snahammed/${service.toLowerCase()}:latest . && docker push snahammed/${service.toLowerCase()}:latest"
                        }
                    }

                    // Use 'dir' step for docker-compose command
                    dir('aitouristguide-backend') {
                        // Bring up Docker containers
                        sh 'docker-compose up -d'
                    }
                }
            }
        }
    }
}
