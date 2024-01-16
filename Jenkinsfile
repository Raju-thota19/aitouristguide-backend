pipeline {
    agent any

    environment {
        M2_HOME = '/opt/apache-maven-3.2.5'
        PATH = "${M2_HOME}/bin:${PATH}"
    }

    tools {
        maven 'Maven-3.2.5'
    }

    stages {
        stage('Build') {
            steps {
                sh 'rm -rf aitouristguide-backend'
                sh 'git clone https://github.com/snahammed506/aitouristguide-backend.git && cd aitouristguide-backend'
            }
        }

        stage('Deploy') {
            steps {
                script {
                    // Your existing deployment steps
                    sh 'cd feedback-service && mvn clean install -DskipTests && docker build -t feedbackimage:latest . && docker push snahammed/feedbackimage:latest'
                    sh 'cd admin-service && mvn clean install -DskipTests && docker build -t adminimage:latest . && docker push snahammed/adminimage:latest'
                    sh 'cd place-service && mvn clean install -DskipTests && docker build -t placeimage:latest . && docker push snahammed/placeimage:latest'
                    sh 'cd server-registry && mvn clean install -DskipTests && docker build -t serverimage:latest . && docker push snahammed/serverimage:latest'
                    sh 'cd tourplan-service && mvn clean install -DskipTests && docker build -t tourplanimage:latest . && docker push snahammed/tourplanimage:latest'
                    sh 'cd UserService && mvn clean install -DskipTests && docker build -t userimage:latest . && docker push snahammed/userimage:latest'
                    sh 'docker-compose up -d'
                }
            }
        }
    }
}
