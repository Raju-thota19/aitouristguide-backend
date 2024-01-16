pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                // Checkout your source code from GitHub
               // git 'https://github.com/snahammed506/aitouristguide-backend.git'
                sh 'git clone https://github.com/snahammed506/aitouristguide-backend.git && cd snahammed506'
            }
        }

        stage('Deploy') {
            steps {
                // withCredentials([usernamePassword(credentialsId: 'DockerRegistry', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                //     sh "docker login -u ${DOCKER_USERNAME} -p ${DOCKER_PASSWORD}"

                    // Feedback Service
                    dir('feedback-service') {
                        sh 'mvn clean install -DskipTests'
                        sh 'docker build -t feedbackimage:latest .'
                        sh 'docker push snahammed/feedbackimage:latest'
                    }

                    // Admin Service
                    dir('admin-service') {
                        sh 'mvn clean install -DskipTests'
                        sh 'docker build -t adminimage:latest .'
                        sh 'docker push snahammed/adminimage:latest'
                    }

                    // Place Service
                    dir('place-service') {
                        sh 'mvn clean install -DskipTests'
                        sh 'docker build -t placeimage:latest .'
                        sh 'docker push snahammed/placeimage:latest'
                    }

                    // Server Registry
                    dir('server-registry') {
                        sh 'mvn clean install -DskipTests'
                        sh 'docker build -t serverimage:latest .'
                        sh 'docker push snahammed/serverimage:latest'
                    }

                    // Tourplan Service
                    dir('tourplan-service') {
                        sh 'mvn clean install -DskipTests'
                        sh 'docker build -t tourplanimage:latest .'
                        sh 'docker push snahammed/tourplanimage:latest'
                    }

                    // User Service
                    dir('UserService') {
                        sh 'mvn clean install -DskipTests'
                        sh 'docker build -t userimage:latest .'
                        sh 'docker push snahammed/userimage:latest'
                    }

                    // Launch all apps
                    sh 'docker-compose up -d'
                }
            }
        }
    }
// }
