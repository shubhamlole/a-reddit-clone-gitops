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
    }
}