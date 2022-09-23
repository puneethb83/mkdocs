pipeline {
environment {
registry = "puneethb83/puneeth-sample-docker"
registryCredential = 'docker_ID'
dockerImage = ''
}
agent any
stages {
stage('Cloning our Git') {
steps {
script{
git 'https://github.com/puneethb83/mkdocs.git'
}
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
            script {
        sh "docker rmi $registry:$BUILD_NUMBER"
}
}
}
}

}
