
@Library("myshare") _
pipeline {
    
     agent { label "ubuntu"}
     
     stages {
         
         stage("ello")
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
                     docker_build("todo-app","latest","abishekchamlagai")
                 }
             }
         }
          stage("push to dockerhub") {
             steps {
                 script{
                     docker_push("todo-app","latest","abishekchamlagai")
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
