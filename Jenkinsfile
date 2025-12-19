pipeline {
    agent any

   stage('Clone Repo') {
    steps {
        git branch: 'main',
            url: 'https://github.com/ARPITDIXIT789/devops-pipeline-checking-.git'
    }
}


        stage('Build Docker Image') {
            steps {
                sh 'docker build -t arpitdixit78/devops-app:latest .'
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub',
                    usernameVariable: 'USER',
                    passwordVariable: 'PASS'
                )]) {
                    sh 'echo $PASS | docker login -u $USER --password-stdin'
                    sh 'docker push arpitdixit78/devops-app:latest'
                }
            }
        }

        stage('Deploy on EC2') {
            steps {
                sh '''
                docker rm -f devops-app || true
                docker run -d -p 80:5000 --name devops-app arpitdixit78/devops-app:latest
                '''
            }
        }
    }
}
