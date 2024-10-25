node('Ubuntu-Appserver-Rebuilt') {

    stage('Cloning Git') {
        // Clone the repository to the workspace
        checkout scm
    }

    stage('Build-and-Tag') {
        // Build the Docker image
        docker.build('akawilk/car_docker_repo')
    }

    stage('Post-to-dockerhub') {
        // Log in to Docker Hub and push the Docker image
        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub_credentials') {
            docker.image('akawilk/car_docker_repo').push('latest')
        }
    }

    stage('Deploy') {
        // Deploy using docker-compose
        sh "docker-compose down"
        sh "docker-compose up -d"
    }
}
