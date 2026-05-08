pipeline {
    agent any
    tools {
        maven 'maven'
        jdk 'jdk17-iti'
    }
   
    stages {
        stage('First stage') {
            steps {
                sh 'date'
                sh 'pwd'
                sh 'ls -ltrha'
            }
        }
        stage('Check version') {
            steps {
            sh 'java -version'
            sh 'mvn -version'
            }
        }
        
        stage('Clone') {
            steps {
                git branch: 'main',
    url: 'https://github.com/spring-projects/spring-petclinic.git'
            }
        }
        stage('Configure port') {
            steps {
                sh 'echo "server.port=9090" >> src/main/resources/application.properties'
            }
        }
        stage('Compile') {
            steps {
                sh 'mvn clean compile'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Package') {
            steps {
                sh 'mvn package'
            }
        }
        stage('Run') {
            steps {
                sh 'nohup java -jar target/*.jar --server.port=9090 > app.log 2>&1 &'
            }
        }
        stage('Sleep') {
            steps {
                sh 'sleep 300'
            }
        }

    }
}
