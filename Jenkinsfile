pipeline {
  agent 
   {
    label 'jenkins-sonarqube-project-node'
   }
  stage('SCM') {
    checkout scm
  }
  stage('SonarQube Analysis') {
    def scannerHome = tool 'SonarScanner';
    withSonarQubeEnv() {
      sh "${scannerHome}/bin/sonar-scanner"
    }
  }
    stage('Build') {
      parallel {
        stage('Build') {
          steps {
            sh 'echo "building the repo in CICD"'
          }
        }
      }
    }

    stage('Test') {
      steps {
        echo "This is test stage -yes"
      }
    }

    stage('Deploy')
    {
      steps {
        echo "deploying the application"
        sh "sudo docker build -t netflix ."
        sh 'sudo docker run -d -p 3000:3000 --name NETFLIX netflix'

      }
    }
}
}
