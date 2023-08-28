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
    stage('SonarQube') {
      def scannerHome = tool 'SonarScanner';
      withSonarQubeEnv() {
        sh "${scannerHome}/bin/sonar-scanner"
      }
    }

    stage('Deploy')
    {
      steps {
        echo "deploying the application"
        sh "sudo docker build -t netflix ."
        sh 'sudo docker run -d -p 80:80 --name NETFLIX netflix'
      }
    }
}
}
