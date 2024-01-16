pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'rm -rf aitouristguide-backend '
                sh 'git clone https://github.com/snahammed506/aitouristguide-backend.git && cd aitouristguide-backend'
            }
        }

        stage('Deploy') {
            steps {
                script {
                    // Feedback Service
                    sh 'cd feedback-service && mvn clean install -DskipTests && docker build -t feedbackimage:latest . && docker push snahammed/feedbackimage:latest'

                    // Admin Service
                    sh 'cd admin-service && mvn clean install -DskipTests && docker build -t adminimage:latest . && docker push snahammed/adminimage:latest'

                    // Place Service
                    sh 'cd place-service && mvn clean install -DskipTests && docker build -t placeimage:latest . && docker push snahammed/placeimage:latest'

                    // Server Registry
                    sh 'cd server-registry && mvn clean install -DskipTests && docker build -t serverimage:latest . && docker push snahammed/serverimage:latest'

                    // Tourplan Service
                    sh 'cd tourplan-service && mvn clean install -DskipTests && docker build -t tourplanimage:latest . && docker push snahammed/tourplanimage:latest'

                    // User Service
                    sh 'cd UserService && mvn clean install -DskipTests && docker build -t userimage:latest . && docker push snahammed/userimage:latest'

                    // Launch all apps
                    sh 'docker-compose up -d'
                }
            }
        }
    }
}
