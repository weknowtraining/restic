// restic
// just run ./docker/build.sh
def label = "docker-${UUID.randomUUID().toString()}"

podTemplate(label: label, inheritFrom: 'base') {
  node(label) {
    stage('Checkout Repository') {
      container('base') {
        checkout scm
      }
    }

    stage('Login to Dockerhub') {
      withCredentials([usernamePassword(credentialsId: 'DockerHub', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
        container('base') {
          sh "docker login --username ${USER} --password ${PASS}"
        }
      }
    }

    stage('Build Docker image') {
      container('base') {
        sh "docker build -f docker/Dockerfile -t weknowtraining/restic:${BRANCH_NAME} -t weknowtraining/restic:latest ."
        sh "docker push weknowtraining/restic:${BRANCH_NAME}"
        sh "docker push weknowtraining/restic:latest"
      }
    }
  }
}
