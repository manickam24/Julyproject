pipeline {
    agent any

    stages {
        stage('Pull Code From GitHub') {
            steps {
                git 'https://github.com/manickam24/Julyproject.git'
            }
        }
        stage('Build the Docker image') {
            steps {
                sh 'sudo docker build -t kubeimage /var/lib/jenkins/workspace/manickam'
                sh 'sudo docker tag kubeimage manickam24/july:latest'
                sh 'sudo docker tag kubeimage manickam24/july:${BUILD_NUMBER}'
            }
        }
        stage('Push the Docker image') {
            steps {
                sh 'sudo docker image push manickam24/july:latest'
                sh 'sudo docker image push manickam24/july:${BUILD_NUMBER}'
            }
        }
        stage('Deploy on Kubernetes') {
            steps {
                sh 'sudo kubectl apply -f /var/lib/jenkins/workspace/manickam/pod.yaml'
                sh 'sudo kubectl rollout restart deployment loadbalancer-pod'
            }
        }
    }
}
