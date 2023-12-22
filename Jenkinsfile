pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                 checkout scmGit(branches: [[name: '*/main']], extensions: [],
userRemoteConfigs: [[url: 'https://github.com/SumitMittal1994/todoapp.git']])
                echo 'successful checkout'
} }
    stage('Build and Package') {
        steps {
            withMaven(maven: 'todo-maven') {
                sh 'mvn clean install'
              echo 'successful Build and Package'
            }
} }
        stage('Build jar and image using Docker file ') {
            steps {
                script {
                     def imageTag = "sumitmittal/todoapp:latest"
                    docker.build(imageTag, '.')
                    echo 'successful Build Docker Image'
                }
} }
        stage('Push to Docker Hub') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker_cred', url: 'https://index.docker.io/v1/') {
                        def imageTag = "sumitmittal/todoapp:latest"
                        docker.image(imageTag).push()
                        echo 'successful Push to Docker Hub'
                    }
} }
}
     stage('Deploy to Kubernetes') {
       steps {
        script {
        // Replace your generated pipeline script here
        kubeconfig(credentialsId: 'kube_config', serverUrl: 
       'https://kubernetes.docker.internal:6443') {
        def kubeConfig = readFile 'kubernetes-config.yaml'
        sh "kubectl apply -f kubernetes-config.yaml"
       }
} }
} 
}
}
