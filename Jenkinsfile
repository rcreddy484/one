pipeline{
    agent any
    parameters {
        string(defaultValue: '', name: 'IMAGE_NAME', description: 'Name of the Docker image to build')
        string(defaultValue: '', name: 'CONTAINER_NAME', description: 'Name of the container to run')
        string(defaultValue: '' , name: 'PORT_NUMBER', description: 'Port number to expose from container')
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'master', url: 'https://github.com/rcreddy484/one.git' // Replace with your actual URL
            }
        }
        stage('Unit Tests') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Build Project') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t ${IMAGE_NAME} .'
            }
        }
        stage('Run Container') {
            steps {
                sh 'docker run -itd --name ${CONTAINER_NAME} -p ${PORT_NUMBER}:8080 ${IMAGE_NAME} '
            }
        }
	tage('Push Docker Image to Docker Registry') {
            steps {
                sh 'docker tag javaimage:latest rcreddy484/docker_practice02:javaimage_prac'
		sh 'docker push rcreddy484/docker_practice02:javaimage_prac'
            }
        }
    }
}
