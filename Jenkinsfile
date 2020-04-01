pipeline {
    agent {
      kubernetes  {
            label 'jenkins-slave'
        }
    }
 
  stages {

      

   stage('Test') {
      environment {
        GIT_CREDS = credentials('github')
        //GITREPO_URL = "github.com/atul7cloudyuga/rsvpapp.git"
        GITREPO_BRANCH = "jenkins-pod-test"
       }
      steps {
           container('python') {
               
               // Set the environment variables
              // sh "export GITREPO_URL=github.com/atul7cloudyuga/rsvpapp.git"
               //sh "export GITREPO_BRANCH=jenkins-pod-test"
               // Clone the git repo
               sh "git clone https://$GIT_CREDS_USR:$GIT_CREDS_PSW@$GITREPO_URL"
               
               dir("rsvpapp") {
                   sh "git checkout $GITREPO_BRANCH"
                   sh  "python -m pip install -r requirements.txt"
                   sh "python -m pytest tests/test_rsvpapp.py"
                }
               
           }
       }
   }
      
      
  }
}
