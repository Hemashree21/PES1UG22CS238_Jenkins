pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building the C++ program...'
                sh 'g++ hello.cpp -o hello'
            }
        }

        stage('Test') {
            steps {
                echo 'Running the compiled program...'
                sh './hello'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying the application... (This is a placeholder)'
            }
        }
    }

    post {
        failure {
            echo 'Pipeline failed'
        }
    }
}

pipeline {
    agent {
        docker {
            image 'node:14'
        }
    }
    stages {
        stage('Clone repository') {
            steps {
                git branch: 'main', url: 'https://github.com/Hemashree21/<repo>.git'
            }
        }
        stage('Install dependencies') {
            steps {
                sh 'npm install'
            }
        }
        stage('Build application') {
            steps {
                sh 'npm run build'
            }
        }
        stage('Test application') {
            steps {
                sh 'npm test'
            }
        }
        stage('Push Docker image') {
            steps {
                sh 'docker build -t <user>/<image>:$BUILD_NUMBER .'
                sh 'docker push <user>/<image>:$BUILD_NUMBER'
            }
        }
    }
}

pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'mvn clean install'
                echo 'Build Stage Successful'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
                echo 'Test Stage Successful'
            }
        }
        stage('Deploy') {
            steps {
                sh 'mvn deploy'
                echo 'Deployment Successful'
            }
        }
    }
    post {
        always {
            junit 'target/surefire-reports/*.xml'
        }
        failure {
            echo 'Pipeline failed'
        }
    }
}
