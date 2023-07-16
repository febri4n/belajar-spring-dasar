pipeline {
    agent {
        node {
            label "linux && java11"
        }
    }
    stages {
        stage("Build") {
            steps {
                echo("Start build")
                sh("./mvnw clean compile test-compile")
                echo("Finish build ")
            }
        }
        stage("Test") {
            steps {
                echo("Start test")
                sh("./mvnw test")
                echo("Finish test ")
            }
        }
        stage("Deploy") {
            steps {
                echo("hello deploy 1")
                sleep(5)
                echo("hello deploy 2")
                echo("hello deploy 3")
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
