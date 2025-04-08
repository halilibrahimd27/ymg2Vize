pipeline {
    agent any
    triggers {
        githubPush()
    }
    environment {
        IMAGE_NAME = "deneme-pipeline"
        CONTAINER_NAME = "nginx-deneme-container"
    }
    stages {
        stage('Repo Klonla') {
            steps {
                git url: 'https://github.com/halilibrahimd27/ymg2Vize.git', branch: 'main'
            }
        }

        stage('Docker Image Olustur') {
            steps {
                echo "Docker Image Olusturuluyor"
                bat "docker build -t %IMAGE_NAME% ."
            }
        }

        stage('Eski Konteyneri Durdur') {
            steps {
                echo "Eski Konteyner Durduruluyor"
                bat "docker rm -f %CONTAINER_NAME% || exit 0"
            }
        }

        stage('Yeni Konteyneri Olustur') {
            steps {
                echo "Yeni Konteyner Olusturuluyor"
                bat "docker run -d --name %CONTAINER_NAME% -p 4444:80 %IMAGE_NAME%"
            }
        }
    }

    post {
        success {
            echo "Yayın başarılı: http://localhost:4444"
        }
        failure {
            echo "Pipeline başarısız oldu."
        }
    }
}
