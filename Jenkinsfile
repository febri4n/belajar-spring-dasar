pipeline {
    agent {
        node {
            label "linux && java11"
        }
    }
    stages {
        stage("Build") {
            steps {
                echo("hello build 1")
                sleep(5)
                echo("hello build 2")
                echo("hello build 3")
            }
        }
        stage("Test") {
            steps {
                echo("hello test 1")
                sleep(5)
                echo("hello test 2")
                echo("hello test 3")
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
