pipeline{
    agent any
    stages{
        stage('git checkoutfile'){
            steps{
                git 'https://github.com/cloudtechmasters/springboohello-CICD.git'
			          //git branch: 'main', url: 'https://github.com/cloudtechmasters/springboohello-CICD.git'
            }
        }
        stage('Build Maven'){
          steps{
              sh 'mvn clean package'
          }
        }
        
        stage("Docker Image"){
            steps{
                sh "docker build -t smvlr/springboohello:${currentBuild.number} ."
            }
        }
        stage("Docker Push"){
        steps{
            withCredentials([usernamePassword(credentialsId: 'docker_credentials', passwordVariable: 'password', usernameVariable: 'username')]) {
                sh "docker login -u ${username} -p ${password}"
            }
            sh "docker push smvlr/springboohello:${currentBuild.number}"
        }
    }
 }
}	
