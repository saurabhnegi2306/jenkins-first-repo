pipeline{
    agent any
    stages {
        stage("Code Build"){
          steps {
             echo "First Step . . . " 
             sh "pwd"
             git branch: 'main', url: 'https://github.com/saurabhnegi2306/jenkins-first-repo/'
          }   
        }
        stage("Image Build"){
          steps {
             echo "Second Step . . . " 
             sh "docker build -t saurabh-app ."
             sh "ls -ltr"
          }  
        }
        stage("Image Push Ongoing"){
          steps {
            echo "Third Step . . . "  
            withCredentials([usernamePassword(credentialsId:"DockerHub", usernameVariable:"DockerHubUser", passwordVariable:"DockerHubPass")]){
              sh "docker tag saurabh-app ${env.DockerHubUser}/saurabh-app:latest  "
              sh "docker login -u ${env.DockerHubUser} -p ${env.DockerHubPass}"
              sh "docker push ${env.DockerHubUser}/saurabh-app:latest"
            }
          }   
        }
        stage("Deploy"){
          steps {
            echo "Fourth Step . . . "
              sh "docker-compose down && docker-compose up -d"
          }   
        }
    }
}
