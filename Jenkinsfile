node {
        stage('pull code from scm'){
            checkout scm
       }
        stage('service and cluster update'){
            sh 'aws s3 cp ./cloudformation/templates/common/ecs-cluster.yaml s3://vikas-cyncproject/cloudformation/templates/common/ecs-cluster.yaml'
            sh 'aws s3 cp ./cloudformation/templates/common/ecs-service.yaml s3://vikas-cyncproject/cloudformation/templates/common/ecs-service.yaml'
            sh 'aws s3 cp ./Jenkinsfile s3://vikas-cyncproject/'
        }

        stage('microservice'){
            sh 'aws --region us-east-1 cloudformation ${Action}-stack --stack-name ${Environment}-${Stack} --template-body file://./cloudformation/templates/microservice.yaml --parameters file://./cloudformation/parameters/${Environment}/microservice.json'
       }

        stage('Stack Status'){
            sh 'aws --region us-east-1 cloudformation wait stack-${Action}-complete --stack-name ${Environment}-${Stack}'
   }
}
