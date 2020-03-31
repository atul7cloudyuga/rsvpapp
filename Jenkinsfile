pipeline {
    agent {
      kubernetes  {
            label 'jenkins-slave'
        }
    }
 
  stages {

      

   stage('Test') {
      environment {
        DOCKERHUB_CREDS = credentials('github')
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
