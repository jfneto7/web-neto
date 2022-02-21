pipeline {
    agent any
    stages{
        
        stage ("Git checkout"){
            steps{
                sh 'ssh root@192.168.2.82 "if [[ -d /opt/web-neto ]];then cd /opt/web-neto && git pull; else cd /opt && git clone https://github.com/jfneto7/web-neto.git;fi"'
            }            
        }

        stage ("Test"){
            steps{
                sh 'ssh root@192.168.2.82 "if [[ -f ./Dockerfile ]];then echo "Dockerfile is here"; else echo "[ERROR] DOCKER IS NOT HERE.........";fi"'
            }            
        }
        
        stage("Build"){
            steps{
                sshCommand remote: root@192.168.2.82, command: "if [[ $(docker container ls | awk {'print $1'}|grep -v CONT) ]];then docker stop $(docker container ls | awk {'print $1'}|grep -v CONT);fi"
            }                       
        }
        
        stage("Deploy"){
            steps{
                sh 'ssh root@192.168.2.82 docker-compose up -d'
            }                       
        }
    }
}
