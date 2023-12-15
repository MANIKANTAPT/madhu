pipeline{
    agent any
    tools{
        maven 'maven'
    }
    stages{
        stage('Build'){
            steps{
                sh 'mvn clean package'
            }
            post{
                success{
                    echo "Archiving the Artifacts"
                    archiveArtifacts artifacts : '/var/lib/jenkins/workspace/pipeline2/target'
                }
            }
        }
        stage('Deploy to Server'){
            steps{
deploy adapters: [tomcat9(credentialsId: '374b7370-3bbc-40d3-ba37-fc19465af689', path: '', url: 'http://15.206.179.200:9090/')], contextPath: null, war: '\'**/*.war\''            }
        }
    }
}
