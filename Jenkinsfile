pipeline {
    agent any

    environment {
        MAVEN_HOME = "/opt/apache-maven"
        PATH = "${MAVEN_HOME}/bin:${env.PATH}"
    }

    stages {
        stage('Clone Repo') {
            steps {
                git url: 'https://github.com/rajatpzade/EasyCRUD.git', branch: 'main'
            }
        }

        stage('Build Backend') {
            steps {
                dir('backend') {
                    sh 'mvn clean package -DskipTests'
                }
            }
        }

        stage('Deploy Backend') {
            steps {
                sh '''
                    echo "Stopping old Spring Boot instance if running..."
                    pkill -f 'student-registration-backend.jar' || true

                    echo "Starting new Spring Boot app..."
                    nohup java -jar backend/target/student-registration-backend.jar > springboot.log 2>&1 &
                '''
            }
        }

        stage('Prepare Frontend') {
            steps {
                dir('frontend') {
                    sh '''
                        echo "Updating apt and installing nodejs, npm..."
                        sudo apt update && sudo apt install -y nodejs npm

                        echo "Installing npm dependencies..."
                        sudo npm install

                        echo 'VITE_API_URL="http://<BACKEND_PUBLIC_IP>:8080/api"' > .env

                        echo "Building frontend..."
                        sudo npm run build
                    '''
                }
            }
        }

        stage('Deploy Frontend') {
            steps {
                sh '''
                    echo "Installing Apache2 server..."
                    sudo apt update && sudo apt install -y apache2

                    echo "Starting Apache2..."
                    sudo systemctl restart apache2

                    echo "Deploying frontend to Apache2..."
                    sudo cp -rf frontend/dist/* /var/www/html/
                '''
            }
        }
    }

    post {
        success {
            echo '✅ End-to-end deployment successful!'
        }
        failure {
            echo '❌ Something failed. Check logs.'
        }
    }
}
