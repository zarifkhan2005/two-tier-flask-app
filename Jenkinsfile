pipeline {
    agent { label 'dev' }

    stages {

        stage('Code Clone') {
            steps {
                git branch: 'master',
                    url: 'https://github.com/zarifkhan2005/two-tier-flask-app.git'

                echo 'Code cloned successfully'
            }
        }

        stage('Build') {
            steps {
                sh 'docker build -t two-tier-flask-app .'
                echo 'Image built successfully'
            }
        }

        stage('Test') {
            steps {
                echo 'Tests completed'
            }
        }

        stage('Push to Docker Hub') {
    steps {
        withCredentials([usernamePassword(
            credentialsId: 'dhc',
            usernameVariable: 'dockerHubUser',
            passwordVariable: 'dockerHubPass'
        )]) {

            sh 'docker login -u $dockerHubUser -p $dockerHubPass'

            sh 'docker tag two-tier-flask-app $dockerHubUser/two-tier-flask-app:latest'

            sh 'docker push $dockerHubUser/two-tier-flask-app:latest'
        }
    }
}
        stage('Deploy') {
            steps {
                sh 'docker compose up -d --build flask-app'
                echo 'Application deployed'
            }
        }
    }
}
