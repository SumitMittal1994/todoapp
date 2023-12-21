pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                 checkout scmGit(branches: [[name: '*/master']], extensions: [],
userRemoteConfigs: [[url: 'https://github.com/SumitMittal1994/todoapp.git']])
                echo 'successful checkout'
} }
        stage('Build jar and image using Docker file ') {
            steps {
                script {
                     def imageTag = "sumitMittal/todoapp:latest"
                    docker.build(imageTag, '.')
                    echo 'successful Build Docker Image'
                }
} }
        stage('Push to Docker Hub') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker_cred', url: 'https://index.docker.io/v1/') {
                        def imageTag = "sumitMittal/todoapp:latest"
                        docker.image(imageTag).push()
                        echo 'successful Push to Docker Hub'
                    }
} }
} }
}
