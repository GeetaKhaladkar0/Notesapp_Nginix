@Library("shared") _

pipeline {
    agent {label 'SlaveNode'}

    stages {
        stage('welcome') {
            steps {
                script{
                    hello()
                }
            }
        }
        stage('Code Clone') {
            steps {
                script{
                    clone("https://github.com/GeetaKhaladkar0/Notesapp_Nginix.git","main")
                }
            }
        }
        stage('Build') {
            steps {
                script{
                    codebuild("notes-app","latest","geetakhaladkar")
                }
            }
        }
        stage('Push Code') {
            steps {
                script{
                    dockerpush("geetakhaladkar","notes-app","latest")
                }
                
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploy code or run code'
                sh "docker compose down && docker compose up -d"
            }
        }
    }
}
