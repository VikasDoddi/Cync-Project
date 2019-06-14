node {  
        stage('pull code from scm'){
            checkout scm
       }
        stage('microservice'){
            sh 'aws --region us-east-1 cloudformation ${Action}-stack --stack-name ${EnvironmentType}-${Stack} --template-body file://./Templates/${Stack}.yml --parameters file://./parameters/${EnvironmentType}/${Stack}.json'
       }

        stage('Stack Status'){
            sh 'aws --region us-east-1 cloudformation wait stack-${Action}-complete --stack-name ${EnvironmentType}-${Stack}'
   }
}
