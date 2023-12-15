pipeline {
    agent any

    tools {
        maven 'maven'
    }

    stages {
        stage('Build') {
            steps {
                script {
                    // Run Maven build
                    sh 'mvn clean package'
                }
            }
            post {
                success {
                    echo "Archiving the Artifacts"
                    archiveArtifacts artifacts: '**/target/*.war', fingerprint: true
                }
            }
        }

        stage('Deploy to Server') {
            steps {
                script {
                    // Define the path to the WAR file
                    def warPath = "/var/lib/jenkins/workspace/pipeline2/target/*.war"
                    
                    // Deploy to Tomcat
                    deploy adapters: [tomcat9(credentialsId: '374b7370-3bbc-40d3-ba37-fc19465af689', path: '', url: 'http://15.206.179.200:9090/')], contextPath: null, war: warPath
                }
            }
        }
    }
}
