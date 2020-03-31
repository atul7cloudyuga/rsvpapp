pipeline {
    agent {
      kubernetes  {
            label 'jenkins-slave'
        }
    }
 
  stages {

    stage('Build') {
      environment {
        DOCKERHUB_CREDS = credentials('dockerhub')
      }
      steps {
        container('docker') {
          // Build new image
          sh "until docker ps; do sleep 3; done && docker build -t atul7cloudyuga/rsvp-demo:${env.GIT_COMMIT} ."
          // Publish new image
          sh "docker login --username $DOCKERHUB_CREDS_USR --password $DOCKERHUB_CREDS_PSW && docker push atul7cloudyuga/rsvp-demo:${env.GIT_COMMIT}"
        }
      }
    }

   stage('Test') {
      environment {
        DOCKERHUB_CREDS = credentials('dockerhub')
       }
      steps {
           container('python') {
               // Clone the git repo
               sh "git clone https://$GIT_CREDS_USR:$GIT_CREDS_PSW@github.com/atul7cloudyuga/rsvpapp.git"
               dir("rsvpapp") {
                   sh "git checkout jenkins-pod-test"
                   sh  "python -m pip install -r requirements.txt"
                   sh "python -m pytest tests/test_rsvpapp.py"
                }
               
           }
       }
   }
      
      
  }
}
