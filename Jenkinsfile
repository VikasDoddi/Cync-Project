node {  
        stage('pull code from scm'){
            checkout scm
       }
        stage('microservice'){
            sh 'aws --region us-east-1 cloudformation ${Action}-stack --stack-name ${Environment}-${Stack} --template-body file://./cloudformation/templates/microservice.yml --parameters file://./cloudformation/parameters/${Environment}/microservice.json'
       }

        stage('Stack Status'){
            sh 'aws --region us-east-1 cloudformation wait stack-${Action}-complete --stack-name ${Environment}-${Stack}'
   }
}
