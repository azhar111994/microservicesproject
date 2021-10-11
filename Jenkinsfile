pipeline {
agent {
label 'build-server'
}

stages {

stage ('Checkout') 
{
steps
    {
    
        checkout scm
        
    }
    
}
stage ('Build') 
{
    steps
    {
       sh "cd /home/ubuntu/workspace/microservices/account-service ; mvn clean install " 
    }
}

   
stage ('dockerimageBuild')
    {
    steps
    {
        sh "cd /home/ubuntu/workspace/microservices/account-service; sudo docker build -t account-service . " 
    }
}
     stage ('dockerimagepush ') 
{
    steps
    {
       sh "cd /home/ubuntu/workspace/microservices/account-service ; sudo  docker login -uazharuddin11 -pAzhar1994 "
        sh "cd /home/ubuntu/workspace/microservices/account-service ; sudo docker tag account-service azharuddin11/account-service "
        sh "cd /home/ubuntu/workspace/microservices/account-service ; sudo docker push azharuddin11/account-service  "
        
        
    }
}
    
    
stage ('k8sdeployment') 
    {
        steps {
            node ('ansible-server') {
             sh " sudo ansible-playbook /ubuntu/k8s.yaml"
   
    }
}
}
}
    
    
}
