pipeline {
    agent any

    tools {
        nodejs 'nodejs'  // Referencing the name you gave in Global Tool Configuration
    }
    
    environment {
        DOCKER_COMPOSE_PATH = "./docker-compose.yml"
    }

    stages {

        stage('Checkout Code') {
            steps {
                echo "Cloning repository..."
                git branch: 'main', url: 'https://github.com/shivamjswlll/Chat-application-Devops-'
            }
        }

        stage('Install Frontend Dependencies') {
            steps {
                echo "Installing frontend dependencies..."
                dir('frontend') {
                    sh 'npm install'
                }
            }
        }

        stage('Install Backend Dependencies') {
            steps {
                echo "Installing backend dependencies..."
                dir('backend') {
                    sh 'npm install'
                }
            }
        }

        stage('Docker Compose Build') {
            steps {
                echo "Building Docker containers..."
                sh "docker-compose -f $DOCKER_COMPOSE_PATH build"
            }
        }

        stage('Docker Compose Up') {
            steps {
                echo "Starting Docker containers..."
                sh "docker-compose -f $DOCKER_COMPOSE_PATH up -d"
            }
        }

    }

    post {
        always {
            echo "Cleaning up unused docker images..."
            sh "docker image prune -af || true"
        }
        success {
            echo "Build completed successfully!"
        }
        failure {
            echo "Build failed!"
        }
    }
}
