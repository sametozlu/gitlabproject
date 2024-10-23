pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                // Docker image oluşturma komutu
                sh 'docker build -t my-app .'
            }
        }

        stage('Test') {
            steps {
                echo 'Testing...'
                // Test komutları, test başarısız olursa pipeline durur
                sh './run-tests.sh'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying...'
                // Docker image'ı kaydetme ve çalıştırma
                sh 'docker run -d my-app'
            }
        }
    }

    post {
        failure {
            mail to: 'test@example.com',
                 subject: "Failed Pipeline: ${currentBuild.fullDisplayName}",
                 body: "Something went wrong with ${env.BUILD_URL}"
        }
    }
}
