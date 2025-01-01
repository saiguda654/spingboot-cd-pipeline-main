pipeline {
    agent { label 'build' }
    parameters {
        string(name: 'IMAGETAG', defaultValue: '1', description: 'Please Enter the Image Tag to Deploy?')
    }
    stages {
        stage('Deploy') {
            steps {
                // Checkout the repository from GitHub using credentials
                git branch: 'main', credentialsId: 'github', url: 'https://github.com/saiguda654/spingboot-cd-pipeline-main.git'
                
                // Modify the deployment.yml file with the image tag
                dir("./kubernetes") {
                    sh "sed -i 's|image: guda654.*|image: guda654/democicd:$IMAGETAG|g' deployment.yml"
                }
                
                // Configure Git user for the commit
                sh '''
                    git config user.name "Jenkins User"
                    git config user.email "jenkins@example.com"
                '''
                
                // Check if there are changes and commit them
                sh 'git diff --quiet || git commit -a -m "New deployment for Build $IMAGETAG"'
                
                // Push changes using the credentials
                withCredentials([usernamePassword(credentialsId: 'github', usernameVariable: 'GIT_USERNAME', passwordVariable: 'GIT_PASSWORD')]) {
                    sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/saiguda654/spingboot-cd-pipeline-main.git main"
                }
            }
        }
    }
}
