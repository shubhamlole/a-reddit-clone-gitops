pipeline{
    agent any
    environment{
        APP_NAME= "reddit-clone-app"
    }
    stages{
        stage("cleanup workspace") {
            steps{
                cleanWs()
            }
        }
        stage("checkout"){
            steps{
                git branch: 'main', credentialsId: 'github', url: 'https://github.com/shubhamlole/a-reddit-clone-gitops.git'
            }
        }
        stage('update Deployment.yml file'){
            steps{
                sh """
                    cat deployment.yml
                    sed -i 's/${APP_NAME}.*/${APP_NAME}:${IMAGE_TAG}/g' deployment.yaml
                    cat deployment.yaml
                   """
            }
        }
        stage('pushed changes to deployment repo'){
            steps{
                sh """
                    git config --global.user.name "shubhamlole"
                    git config --global.user.email "loleshubham46@gmail.com"
                    git add deployment.yml
                    git commit -m "deployment.yml file updated" 
                   """
                   withCredentials([gitusernamePassword:'github', gitToolName: 'Default']){
                   sh "git push https://github.com/shubhamlole/a-reddit-clone-gitops.git"
                   }
            }
        }
    }
}