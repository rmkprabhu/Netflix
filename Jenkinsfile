pipeline {
  agent 
   {
    label 'sonarqube-netflix'
   }
  stages {
    stage('Build') {
      parallel {
        stage('Build') {
          steps {
            sh 'echo "building the repo in jenkins server iafter installing docker and git in server"'
          }
        }
      }
    }

    stage('Test') {
      steps {
        echo "This is test stage -yes"
      }
    }
    stage('sonarqube') {
      environment {
        scannerHome = tool 'Sonar-scanner'
      }
      steps {
      
      withSonarQubeEnv('Sonar-scanner') {
        sh "${scannerHome}/bin/sonar-scanner"
        }
      }
    }

    stage('Deploy')
    {
      steps {
        echo "removing existing containers to avoid conjunction"
        sh "sudo docker rm $(docker ps -aq)"
        echo "building docker image"
        sh "sudo docker build -t netflix ."
        echo "deploying the application"
        sh 'sudo docker run -d -p 80:80 --name NETFLIX netflix'
      }
    }
}
}
