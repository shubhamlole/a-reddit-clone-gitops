pipeline{
    agent any
    environment{
        APP_NAME = "reddit-clone-pipeline"
    }
    stages{
        stage("Cleanup workspace"){
            steps{
                cleanWs()
            }
        }
        stage("cd repo clone"){
            steps{
                git branch: 'main', credentialsId: 'github', url:'https://github.com/shubhamlole/a-reddit-clone-gitops.git'
            }
        }
        stage("Update the Deployment Tags") {
            steps {
                sh """
                    cat deployment.yml
                    sed -i 's/${APP_NAME}.*/${APP_NAME}:${IMAGE_TAG}/g' deployment.yml
                    cat deployment.yml
                """
            }
         }
         stage("Push the changed deployment file to GitHub") {
            steps {
                sh """
                    git config --global user.name "shubhamlole"
                    git config --global user.email "loleshubham46@gmail.com"
                    git add deployment.yml
                    git commit -m "Updated Deployment Manifest"
                """
                withCredentials([gitUsernamePassword(credentialsId: 'github', gitToolName: 'Default')]) {
                    sh "git push https://github.com/shubhamlole/a-reddit-clone-gitops.git main"
                }
            }
         }
    }
}