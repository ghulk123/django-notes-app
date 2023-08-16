pipeline {
    agent any
    
        stages{
            stage("Clone code"){
                steps{
                    echo "Cloning the code perfectly"
                    git url: "https://github.com/ghulk123/django-notes-app.git" , branch:"main"
                }
            }
            stage("Build"){
                steps{
                    echo "Building the image"
                    sh "docker build -t my-note-app ."
                }
            }
            stage("Push To Docker Hub"){
                steps{
                    echo "Pushing the image to docker hub"
                    withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                    sh "docker tag my-note-app ${env.dockerHubUser}/my-note-app:latest"    
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                    sh "docker push ${env.dockerHubUser}/my-note-app:latest"
                    }
                }
            }
            stage("Deploy"){
                steps{
                    echo "Deploying the container"
                    sh "docker-compose down && docker-compose up -d"
                }
            }
        }
}
