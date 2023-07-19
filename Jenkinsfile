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

    parameters {
        string(name: "NAME", defaultValue: "Guest", description: "What is your name?")
        text(name: "DESCRIPTION", defaultValue: "Guest", description: "Tell me about you")
        booleanParam(name: "DEPLOY", defaultValue: false, description: "Need to Deploy?")
        choice(name: "SOCIAL_MEDIA", choices: ['Instagram', 'Facebook', 'Twitter'], description: "Which Social Media?")
        password(name: "SECRET", defaultValue: "", description: "Encrypt Key")
    }

    stages {
        stage("Parameter") {
            agent {
                node {
                    label "linux && java11"
                }
            }
            steps {
                echo "Hello ${params.NAME}"
                echo "You description is ${params.DESCRIPTION}"
                echo "Your social medis is ${params.SOCIAL_MEDIA}"
                echo "Need to deploy : ${params.DEPLOY} to deploy!"
                echo "Your secret is ${params.SECRET}"
            }
        }
        
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
