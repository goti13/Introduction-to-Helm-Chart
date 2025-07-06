pipeline {
    agent any

    triggers {
        githubPush()
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Deploy with Helm') {
            steps {
                script {
                    sh '/usr/local/bin/helm upgrade --install my-webapp ./webapp --namespace default --create-namespace'
                }
            }
        }
    }

    post {
        success {
            echo '✅ Helm deployment succeeded.'
        }
        failure {
            echo '❌ Helm deployment failed.'
        }
    }
}
