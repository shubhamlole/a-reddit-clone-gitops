pipeline{
    agent any
    environment{
        APP_NAME = "reddit-clone-app"
    }
    stages{
        stage("Cleanup Workspace"){
            steps{
                cleanWs()
            }
        }
        stage("checkout scm"){
            steps{
                git branch: 'main' , credentialsId: 'github' , url: 'https://github.com/shubhamlole/a-reddit-clone-gitops.git'
            }
        }
        stage("Update Deployment file"){
            steps{
                sh """
                cat deployment.yaml
                sed -i 's/${APP_NAME}.*/${APP_NAME}:${IMAGE_TAG}/g' deployment.yaml
                    cat deployment.yaml
                """
            }
        }
        stage("push the changes deployment file to github"){
            steps{
                sh """
                git config --global user.name "shubhamlole"
                git config --global user.email "loleshubham46@gmail.com"
                git add deployment.yaml
                git commit -m "updated manifest file" 
                """
                withCredentials([gitUsernamePassword(credentialsId: 'github', gitToolName: 'Default')]) {
                    sh "git push https://github.com/shubhamlole/a-reddit-clone-gitops main"
                }
            }
        }
    }
}