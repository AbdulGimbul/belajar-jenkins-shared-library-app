pipeline {
    agent any

    environment {
        AUTHOR = "Muhamad Abdul Aziz"
        EMAIL = "azizgimboell@gmail.com"
        WEB = "https://www.alterdev.id/portfolio-abdul"
    }

//     triggers {
//         cron("*/5 * * * *")
//         pollSCM("*/5 * * * *")
//     }

    parameters {
        string(name: "NAME", defaultValue: "Guest", description: "What is your name?")
        text(name: "DESCRIPTION", defaultValue: "Guest", description: "Tell me about you")
        booleanParam(name: "DEPLOY", defaultValue: false, description: "Need to Deploy?")
        choice(name: "SOCIAL_MEDIA", choices: ['Instagram', 'Facebook', 'Twitter'], description: "Which Social Media?")
        password(name: "SECRET", defaultValue: "", description: "Encrypt Key")
    }

    stages {
        stage("Parameter") {
            environment {
                APP = credentials("abdl_rahasia")
            }
            steps {
                echo "Hello ${params.NAME}"
                echo "Your description is ${params.DESCRIPTION}"
                echo "Your social media is ${params.SOCIAL_MEDIA}"
                echo "Need to deploy : ${params.DEPLOY} to deploy!"
                echo "Your secret is ${params.SECRET}"
            }
        }
        stage("Prepare") {
            environment {
                APP = credentials("abdl_rahasia")
            }
            steps {
                echo("Author ${AUTHOR}")
                echo("Email ${EMAIL}")
                echo("Start Job : ${env.JOB_NAME}")
                echo("Start Build : ${env.BUILD_NUMBER}")
                echo("Branch Name : ${env.BRANCH_NAME}")
                echo("App User : ${APP_USR}")
                sh('echo "App Password : $APP_PSW" > "rahasia.txt"')
            }
        }
        stage("Build") {
            steps {
                script {
                    for(int i = 0; i < 10; i++){
                        echo("Script ${i}")
                    }
                }

                echo("Start Build")
                sh("./mvnw clean compile test-compile")
                echo("Finish Build")
            }
        }
        stage("Test"){
            steps {
                script {
                    def data = [
                        "firstName" : "Abdul",
                        "lastName" : "Aziz"
                    ]
                    writeJSON(file: "data.json", json: data)
                }
                echo("Start Test")
                sh("./mvnw test")
                echo("Finish Test")
            }
        }
        stage("Deploy"){
            input {
                message "Can we deploy?"
                ok "Yes, of course"
                submitter "pzn, abdl"
                parameters {
                    choice(name: "TARGET_ENV", choices:['DEV', 'QA', 'PROD'], description: "Which Environment?")
                }
            }
            steps {
                echo "Hello Deploy 1"
                sleep(5)
                echo "Hello Deploy 2"
                echo "Hello Deploy 3"
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