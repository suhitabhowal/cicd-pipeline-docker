pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                sh './gradlew build --no-daemon'
                archiveArtifacts artifacts: 'dist/trainSchedule.zip'
            }
        }
        
        stage('Build Docker image'){
            
           /* when{
			branch 'master'
		}*/
                                   
            steps {
                script {
                    app = docker.build("suhita/node-app")
                    app.inside {
                        sh 'echo $(curl localhost:8081)'
                    }
                }
            }
            
        }
        
        stage('Push docker image'){
           /*when{
			branch 'master'
			}*/
            steps{
                script {
                    docker.withRegistry('https://registry.hub.docker.com','DockerHub_ID'){
                        app.push("${env.BUILD_NUMBER}")
                        app.push("latest")
                    }
                }
            }
        }
        
    }
}

