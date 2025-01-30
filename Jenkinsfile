
@Library("Shared") _
pipeline {
    
     agent { label "test"}
     
     stages {
         
         stage("hello")
         {
             steps{
                 script{
                    hello()
                 }
             }
         }
         
         stage("code") {
             steps {
                script{
                    clone("https://github.com/abi123shek/node-todo-cicd.git","master")
                 
                }
             }
         }
         stage("build") {
             steps {
                 
                 script{
                     docker_build("todo-app-v1.1","latest","abishekchamlagai")
                 }
             }
         }
                   stage("push to dockerhub") {
             steps {
                  echo "Connecting to docker hub"
                  withCredentials([usernamePassword('credentialsId':"DockerConfig", 
                  passwordVariable:"DockerConfigpass", usernameVariable:"DockerConfigUser")]){
                      
                 sh "docker login -u ${env.DockerConfigUser} -p ${env.DockerConfigpass}" 
                 sh "docker image tag todo-app:latest  ${env.DockerConfigUser}/todo-app:latest"
                 sh "docker push ${env.DockerConfigUser}/todo-app:latest"
                 echo "Node.js application deployed successfully"
                  }
             }
         }

         
         
         

         stage("deploy") {
             steps {
                 sh "docker-compose down && docker-compose up -d" 
                 echo "Node.js application deployed successfully"
             }
         }
    }
}
