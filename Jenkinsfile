pipeline {
    agent any
    stages {
        stage('Hello') {
            steps {
                echo 'Hello Pipeline!'
            }
        }
    }
    post {
        always {
            echo "I will always Hello again!"
        }
        success {
            echo "Yay, success!"
        }
        failure {
            echo "Oh no, failure"
        }
        cleanup {
            echo "Don't care success or error"
        }
    }
}