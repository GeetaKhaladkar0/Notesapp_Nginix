pipeline{
    
    agent any
    
    stages{
        
        stage("code"){
            steps{
                 echo "cloning  a code" 
                 git url: "https://github.com/GeetaKhaladkar0/Notesapp_Nginix.git", branch: "main"
            }
          
        }
        stage("build"){
            steps{
                echo "build a code"
                sh "docker build . -t mynotesapp"
            }
            
        }
        stage("push to dockerhub"){
            steps{
                echo "pushing the image to dockerhub"
                withCredentials([usernamePassword( credentialsId: "dockerhub", usernameVariable: "dockerhubuser", passwordVariable: "dockerhubpass")])
                {
                    sh "docker tag mynotesapp ${env.dockerhubuser}/mynotesapp:latest "
                    sh "docker login -u ${env.dockerhubuser} -p ${env.dockerhubpass}"
                    sh "docker push ${env.dockerhubuser}/mynotesapp:latest"
                }

                
                
            }
            
        }
        stage("deploy on aws"){
            steps{
                 echo "deploy container"
                 sh "docker-compose down && docker-compose up -d"
            }
           
        }
    }
}
