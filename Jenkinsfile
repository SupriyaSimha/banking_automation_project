pipeline {
    agent any
    stages{
        stage('git cloned'){
            steps{
                git url:'https://github.com/SupriyaSimha/banking_automation_project/', branch: "master"
              
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t supriyasimha/staragilebankingproject:v1 .'
                    sh 'docker images'
                }
            }
        }
          stage('Docker login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-pwd', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                    sh "echo $PASS | docker login -u $USER --password-stdin"
                    sh 'docker push supriyasimha/staragilebankingproject:v1'
                }
            }
        }
        
     stage('Deploy') {
            steps {
               sh 'sudo docker run -itd --name My-first-containe2211 -p 8083:80 supriyasimha/staragilebankingproject:v1'
            }
        }
    }
}