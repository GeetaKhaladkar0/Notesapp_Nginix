pipeline{
    agent any
    stages{
        stage("CODE"){
            steps{
                echo "clone code from github"
                git url : "https://github.com/GeetaKhaladkar0/Notesapp_Nginix.git" , branch : "main"
            }
            
            
        }
        stage("BUilD"){
             steps{
                 echo "building the image"
                 sh "docker build . -t notesapplication"
            }
           
            
        }
        stage("PUSH IMAGE ON DOCKERHUB"){
             steps{
                echo "push image"
                 withCredentials([usernamePassword( credentialsId: "dockerhub", usernameVariable: "dockerhubuser", passwordVariable: "dockerhubpass")])
                {
                    sh "docker tag notesapplication  ${env.dockerhubuser}/notesapplication:latest "
                    sh "docker login -u ${env.dockerhubuser} -p ${env.dockerhubpass}"
                    sh "docker push  ${env.dockerhubuser}/notesapplication:latest "
                }

            }
            
            
        }
        stage("DEPLOY ON AWS"){
             steps{
                echo "deploy container"
                sh "docker-compose down && docker-compose up -d "
            }
            
        }
    }
}
    
