pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                build 'PES1UG22CS238-1'
                sh 'g++ main.cpp -o output'
            }
        }
        stage('Test') {
            steps {
                sh './output'
            }
        }
        stage('Deploy') {
            steps {
                echo 'deploy'
            }
        }
    }
    post {
        failure {
            error 'Pipeline failed'
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
