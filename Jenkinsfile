pipeline{
     agent any
environment{
DOCKER_IMAGE = "gunapriyaguna2006/new-image"
}
stages{
 stage('Clone Repository'){
 git 'https://github.com/gunapriyaguna2006/program4.git'
}
}
stage('Build Docker Image'){
steps{
   script{
      docker.build("$(DOCKER_IMAGE):v1")
}
}
}
stage('Login to Docker Hub'){
steps{
 withCredentials([usernamePassword(credentialsId: 'dockerhub-creds',
usernameVariable: 'Docker_USER',passwordVariable:'DOCKER_PASS')]){
 bat 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
}
}
}
stage('push Docker Image'){
 steps{
 script{
 docker.withregistry('','dockerhub-creds'){
  docker.image("$DOCKER_IMAGE):v1").push()
}
}
}
}
}
post{
success{
 echo 'Image successfully built and pushed to Docker Hub'
}
failure{
 echo 'Pipeline failed'
}
}
}


