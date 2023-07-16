pipeline {
    agent {
        node {
            label "linux && java11"
        }
    }
    stages {
        stage("Build") {
            steps {
                echo("hello build")
            }
        }
        stage("Test") {
            steps {
                echo("hello test")
                sh("error")
            }
        }
        stage("Deploy") {
            steps {
                echo("hello deploy")
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
