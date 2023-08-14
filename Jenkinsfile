pipeline {
  agent 
   {
    label 'jenkins-sonarqube-project-node'
   }
  stages {
    stage('SCM') {
    git 'https://github.com/rmkprabhu/Netflix.git'
  }
  stage('SonarQube analysis') {
    def scannerHome = tool 'SonarScanner 4.0';
    withSonarQubeEnv('Sonar-scanner') { // If you have configured more than one global server connection, you can specify its name
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
