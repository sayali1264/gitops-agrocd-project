pipeline {
    agent any

    environment{
            DOCKERHUB_USERNAME ="sayali1264"
            APP_NAME = "gitops-argo-app"
            IMAGE_TAG = "${BUILD_NUMBER}"
            IMAGE_NAME = "${DOCKERHUB_USERNAME}" +"/"+"${APP_NAME}"
            REGISTRY_CREDS = 'dockerhub'

    
    }

    stages {
        stage('Cleanup workspace') {
            steps {
                script {
                    cleanWs()
                }
            }
        }

   stage('Checkout SCM') {
     steps {
        git credentialsId: 'github',
        url: 'https://github.com/sayali1264/gitops-agrocd-project.git',
        branch: 'main'
  }
}

stage('Build Docker Image') {
    steps {
        script {
            docker_image = docker.build("${IMAGE_NAME}")
        }
    }
}

stage('Push Docker Image') {
    steps {
        script {
            docker.withRegistry('', REGISTRY_CREDS) {
                docker_image.push("$BUILD_NUMBER")
                docker_image.push('latest')
            }
        }
    }
}





    }
}