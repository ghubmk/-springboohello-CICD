pipeline{
    agent any
    stages{
        stage('git checkoutfile'){
            steps{
		sh "git clone --single-branch --branch ${params.branch} ${params.cloneUrl} ${params.tag}"	
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
