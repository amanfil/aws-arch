node {

	def REGION = "us-west-2"
	def CLUSTER = "default"
	def SERVICE_NAME = "${NAME}-service"
	def NAME = " "
	
    stage('Clone repository') {
        git branch: "master", url: "https://github.com/amanfil/${APP_NAME}.git"
    }
               
    stage('Retrieve an auth token and Authenticate Docker Client') {
         withAWS(credentials: 'ecs-user')
             {
               sh  "aws ecr get-login-password --region us-west-2 | docker login --username AWS --password-stdin 482673545144.dkr.ecr.us-west-2.amazonaws.com/${APP_NAME} "
        }
    }
    stage('Build Docker Image') {
         sh 'docker build -t ${APP_NAME} .'
    }
    
    stage('Build Docker Tag') {
         sh 'docker tag ecs-demo-app:latest ${APP_NAME}'
    }
    
    stage('Push Docker Image') {
         sh 'docker push ${APP_NAME}'
    }
    
   
    stage('Deploy') {
         withAWS(credentials: 'ecs-user',region:'us-west-2')
             {
               $(Deployment of Service and DB)
    }
}
