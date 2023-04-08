pipeline {
  tools {
    nodejs 'node'
  }
  stages {
    stage ('Build') {
       steps {
                git 'https://github.com/suryaops22/Sample-NodeJS.git'
                CMD {'npm install'}
      steps {
        sh 'printenv'
      }
    }
    stage ('Publish ECR') {
      steps {
        withEnv (["AWS_ACCESS_KEY_ID=$(env.AWS_ACCESS_KEY_ID)", "AWS_SECRET_ACESS_KEY=$(env.AWS_SECRET_ACESS_KEY)", "AWS_DEFAULT_REGION=$(env.AWS_DEFAULT_REGION)"]) {
          sh 'docker login -u AWS -p $(aws ecr get-login-password --region us-east-1) 742774316769.dkr.ecr.us-east-1.amazonaws.com'
          sh 'docker build -t sample-app:1.0 .'
          sh 'docker tag sample-app:1.0 742774316769.dkr.ecr.us-east-1.amazonaws.com/sample-app:1.0'
          sh 'docker push 742774316769.dkr.ecr.us-east-1.amazonaws.com/sample-app:1.0'
        }
      }
    }
  }
}

          
