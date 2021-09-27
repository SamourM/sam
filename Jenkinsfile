pipeline {
  agent any
 
  stages {
    stage('Build') {
      steps {
        sh 'sam build'
      }
    }
    stage('beta') {
      environment {
        STACK_NAME = 'sam-app-beta-stage'
        S3_BUCKET = 'sam-jenkins-demo-us-west-2-samour'
      }
      steps {
        withAWS(credentials: 'sam-jenkins-demo-credentials', region: 'us-west-2') {
          sh 'sam deploy --stack-name $STACK_NAME -t template.yaml --s3-bucket $S3_BUCKET --capabilities CAPABILITY_IAM'
        }
      }
    }
  }
}
