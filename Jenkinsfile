pipeline {
 agent { label 'build' }
 parameters {
     password(name: 'PASSWD', defaultValue: '', description: 'Please Enter your GitHub password')
     string(name: 'IMAGETAG', defaultValue: '1', description: 'Please Enter the Image Tag to Deploy?')
 }
 stages {
  stage('Deploy')
  {
    steps { 
        git branch: 'main', credentialsId: 'GitHubCred', url: 'https://github.com/saiguda654/spingboot-cd-pipeline-main.git'
      dir ("./kubernetes") {
              sh "sed -i 's/image: guda654.*/image: guda654\\/wezvatechbackend:$IMAGETAG/g' deployment.yml" 
	    }
	    sh 'git commit -a -m "New deployment for Build $IMAGETAG"'
	    sh "git push https://github.com/saiguda654/spingboot-cd-pipeline-main.git"
    }
  }
 }
}
