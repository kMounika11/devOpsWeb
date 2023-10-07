pipeline{
    agent any
    tools{
        maven 'MAVEN_HOME'
    }
    stages{
        stage('Build'){
            steps{
                bat 'mvn clean package'
            }
            post{
                success{
                    echo "Archiving artifacts"
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage ('Deploy to Tomcat Server'){
            steps {
                echo "Deply to tomcat server"
                deploy adapters: [tomcat9(credentialsId: 'tomcat', path: '', url: 'http://localhost:8081/manager/html')], contextPath: null, war: '**/*.war'
            }
        }
    }
}

