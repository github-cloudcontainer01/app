pipeline {

    agent any

    environment {
        IMAGE = "dpravin7/sample-app"
    }

    stages {
        stage('Checkout') {
    steps {
        git branch: 'main', credentialsId: 'git_creds',
            url: 'https://github.com/github-cloudcontainer01/app.git'
         }
    }

        stage('Build Docker Image') {

            steps {
                sh 'docker build -t $IMAGE:latest .'
            }

        }

        stage('Run Tests') {

            steps {
                sh 'npm install'
                sh 'npm test'
            }

        }

        stage('Push Image') {

            steps {

                withCredentials([usernamePassword(credentialsId:'docker_creds',

                usernameVariable:'USER',

                passwordVariable:'PASS')]) {

                    sh '''
                    echo $PASS | docker login -u $USER --password-stdin
                    docker push $IMAGE:latest
                    '''
                }

            }

        }

        stage('Deploy') {

            steps {

                sh 'kubectl apply -f deployment.yaml'

                sh 'kubectl apply -f service.yaml'

            }

        }

    }

}
