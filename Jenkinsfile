pipeline {
    agent {
        node {
            label "linux && java11"
        }
    }
    stages {
        stage("hello") {
            steps {
                echo("hello pipeline")
            }
        }
    }
    post {
        always {
            echo "i always say hello again!"
        }    
        success {
            echo "ye, success"
        }
        failure {
            echo "oh no, failure"
        }
        cleanup {
            echo "dont care success or error"
        }
    }
}
