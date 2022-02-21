def remoteHost = "192.168.2.82"
pipeline {
    agent any
    stages{
        
        stage ("Git checkout"){
            steps{
                sh 'ssh root@${remoteHost} cd /opt'
                sh 'ssh root@${remoteHost} "git clone https://github.com/jfneto7/web-neto.git"'
            }            
        }

        stage ("Test"){
            steps{
                sh 'ssh root@${remoteHost}  "if [[ -f ./Dockerfile ]];then echo "Dockerfile is here"; else echo "[ERROR] DOCKER IS NOT HERE.........";fi"'
            }            
        }
        
        stage("Deploy"){
            steps{
                sh 'ssh root@${remoteHost} docker-compose up'
            }                       
        }
    }
}
