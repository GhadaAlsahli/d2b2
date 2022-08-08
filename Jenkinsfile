pipeline {

    agent any

    stages {

        stage('Quality Scan') {
            steps {
               
            sh "mvn -Dmaven.test.failure.ignore=true clean compile"
               
            sh "mvn clean verify sonar:sonar \
  -Dsonar.projectKey=onsite-GhadaAlsahli-B2D2 \
  -Dsonar.host.url=http://52.23.193.18 \
  -Dsonar.login=sqp_4f23159408f6a962bdc32f98e4fc585741dedba5"

               
            }

            
        }

        stage('Build'){
            steps {
                sh "mvn clean"

                sh "mvn compile"
            }
        }

        stage('Test'){
            steps {
                sh "mvn test"
            }

            post {
                always {
                    junit '/target/surefire-reports/TEST-*.xml'
                }
            }
        }

        stage('Package'){
            steps {
                
                sh "mvn package"
            }
            post {
                always {
                    junit '/target/surefire-reports/TEST-*.xml'
                }
                success {
                    
                    archiveArtifacts 'target/*.jar'
        
                }
            }
        }

    }

}

