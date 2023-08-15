pipeline {
  agent any

  stages {
    stage('Build') {
      steps {
        sh 'docker build -t flask_application .'
        sh 'docker tag flask_application $Docker_Flask_Image'
      }
    }
    stage('Test') {
      steps {
        sh 'docker run flask_application python -m pytest app/tests/'
      }
    }
    stage('Deploy') {
      steps {
        withCredentials([usernamePassword(credentialsId: "${Docker_Cred}", passwordVariable: 'DOCKER_PASSWORD', usernameVariable: 'DOCKER_USERNAME')]) {
          sh "echo \$DOCKER_PASSWORD | docker login -u \$DOCKER_USERNAME --password-stdin docker.io"
          sh 'docker push $Docker_Flask_Image'
        }
      }
    }
  }
  post {
    always {
      sh 'docker logout'
    }
  }
}
