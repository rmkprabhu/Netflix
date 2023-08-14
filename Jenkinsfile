pipeline {
  agent 
   {
    label 'bpcl-prod'
   }
  stages {
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
        sh "sudo docker build -t python-testjenkins ."
        sh 'sudo docker run -d -p "5000:5000" -i python-testjenkins:latest'
      }
    }
}
}
