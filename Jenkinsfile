pipeline {
    agent any

    stages {
        stage('Install Maven') {
            steps {
                sh '''
                    wget https://archive.apache.org/dist/maven/maven-3/3.2.5/binaries/apache-maven-3.2.5-bin.tar.gz
                    tar -xf apache-maven-3.2.5-bin.tar.gz
                    sudo mv apache-maven-3.2.5 /opt/
                    echo "export MAVEN_HOME=/opt/apache-maven-3.2.5" >> ~/.bashrc
                    echo "export PATH=\$MAVEN_HOME/bin:\$PATH" >> ~/.bashrc
                    source ~/.bashrc
                '''
            }
        }

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
