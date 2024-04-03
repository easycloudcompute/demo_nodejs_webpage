pipeline {
    agent {label 'master'}
    
    environment {
    PATH="/opt/maven/bin:/opt/node-v21.7.1-linux-arm64/bin:$PATH"
    }

    stages {
        
        stage('install dependencies') {
            steps {
                sh "/opt/node-v21.7.1-linux-arm64/bin/npm install"
            }
        }
        
        stage('Docker Build and Push') {
            steps {
               script {
                   withDockerRegistry(credentialsId: 'a58c5723-67bd-45cb-8048-ef672b603980', toolName: 'docker') {
                       
                    sh "docker build -t nodejsapp01-image ."
                    sh "docker tag nodejsapp01-image rahulunixsa87/nodejs01app:latest"
                    sh "docker push rahulunixsa87/nodejs01app:latest"
                    
                   }
                 }
               }
            }
            
            stage('Docker Deploy') {
            steps {
               script {
                   withDockerRegistry(credentialsId: 'a58c5723-67bd-45cb-8048-ef672b603980', toolName: 'docker') {
                       
                    sh "docker run -d --name nodejs01app -p 8081:8081 rahulunixsa87/nodejs01app:latest"
                    
                   }
                 }
               }
            }
            
    }
}
