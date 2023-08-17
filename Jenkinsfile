pipeline {
    agent { label 'dev-agent' }
    
        stage('code'){
            steps {
                git url: 'https://github.com/AkshayShelke3001/node-todo-cicd.git', branch: 'dev'
            }
        }
        stage('build and test'){
            steps {
                sh 'docker build . -t akkishelke/node-todo-app-cicd:latest'
            }
        }
        stage('login and push image'){
            steps {
                echo 'login into dockerhub and pushing image'
                withCredentials([usernamePassword(credentialsId:'dockerhub',passwordVariable:'dockerhubPassword',usernameVariable:'dockerhubUser')]){
                    sh "docker login -u ${env.dockerhubUser} -p ${env.dockerhubPassword}"
                    sh "docker push akkishelke/node-todo-app-cicd:latest"
                }
            }
        }
         stage('Deploy'){
            steps {
                sh 'docker-compose down && docker-compose up -d --no-deps --build web'
            }
        }     
        stage("Deploy"){
            steps{
                sh "docker-compose down && docker-compose up -d --no-deps --build web"
            }
        }
    }
}
