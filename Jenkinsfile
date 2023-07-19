pipeline {
    agent none

    environment {
        AUTHOR = "Febrian"
        BLOG = "https://febri4n.github.io/blog/"
    }

    options {
        disableConcurrentBuilds()
        timeout(time: 10, unit: 'SECONDS')
    }

    stages {
        
        stage("Prepare") {
            environment {
                APP = credentials("febrian_rahasia")
            }
            agent {
                node {
                    label "linux && java11"
                }
            }
            steps {
                echo("App User: ${APP_USR}")
                echo("App Password: ${APP_PSW}")
                sh('echo "App Password: {APP_PSW}" > "rahasia.txt"')
                echo("Author: ${AUTHOR}")
                echo("Blog URL: ${BLOG}")
                echo("Start job: ${env.JOB_NAME}")
                echo("Start build: ${env.BUILD_NUMBER}")
                echo("Branch name: ${env.BRANCH_NAME}")
            }
        }
        
        stage("Build") {
            agent {
                node {
                    label "linux && java11"
                }
            }
            steps {
                script {
                    for (int i = 0; i<10; i++) {
                        echo("Script ${i}")
                    }
                }

                echo("Start build")
                sh("./mvnw clean compile test-compile")
                echo("Finish build ")
            }
        }
        
        stage("Test") {
            agent {
                node {
                    label "linux && java11"
                }
            }  
            steps { 
                script {
                    def data = [
                        "firstName" : "Febrian",
                        "lastName" : "Saputra"
                    ]
                    writeJSON(file: "data.json", json: data)
                }
                echo("Start test")
                sh("./mvnw test")
                echo("Finish test ")
            }
        }
        
        stage("Deploy") {
            agent {
                node {
                    label "linux && java11"
                }
            }
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
