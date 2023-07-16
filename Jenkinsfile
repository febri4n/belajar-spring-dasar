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
}
