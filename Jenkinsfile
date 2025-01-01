pipeline {
    agent { label 'build' }
    parameters {
        password(name: 'PASSWD', defaultValue: '', description: 'Please Enter your GitHub password')
        string(name: 'IMAGETAG', defaultValue: '1', description: 'Please Enter the Image Tag to Deploy?')
    }
    stages {
        stage('Deploy') {
            steps { 
                // Checkout the repository from GitHub
                git branch: 'main', credentialsId: 'GitHubCred', url: 'https://github.com/saiguda654/spingboot-cd-pipeline-main.git'
                
                // Modify the deployment.yml file with the image tag
                dir("./kubernetes") {
                    sh "sed -i 's/image: guda654.*/image: guda654\\/wezvatechbackend:$IMAGETAG/g' deployment.yml" 
                }
                
                // Check if there are changes and commit them
                sh 'git diff --exit-code || git commit -a -m "New deployment for Build $IMAGETAG"'
                
                // Push changes to GitHub
                sh "git push origin main"
            }
        }
    }
}
