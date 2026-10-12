pipeline {
    agent any

    tools {
        jdk 'jdk21'        // match Java 21 installed on the host
        nodejs 'node23'
    }

    stages {
        stage('Clean Workspace') {
            steps { cleanWs() }
        }

        stage('Checkout from Git') {
            steps {
                git 'https://github.com/malvihuzefa8/project-swiggy.git'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t swiggy:latest .'
            }
        }

        stage('Deploy to Container') {
            steps {
                sh '''
                    docker stop swiggy || true
                    docker rm swiggy || true
                    docker run -d --name swiggy -p 3000:3000 swiggy:latest
                '''
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}
