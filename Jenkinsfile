pipeline {
environment {
registry = "kausvaibhav/docker-repo-for-maven-build"
registryCredential = 'docker-creds'
dockerImage = ''
}
agent any
stages {
stage('Cloning our Git') {
steps {
git 'https://github.com/kaushikk007/mkdocs.git'
}
}
stage('Building our image') {
steps{
script {
dockerImage = docker.build registry + ":$BUILD_NUMBER"
}
}
}
stage('Deploy our image') {
steps{
script {
docker.withRegistry( '', registryCredential ) {
dockerImage.push()
}
}
}
}
stage('Remove Unused docker image') {
      steps{
        sh "docker rmi $registry:$BUILD_NUMBER"
}
}
}

