pipeline {
  agent { label 'linux'}
  options {
    skipDefaultCheckout(true)
  }
  stages{
    stage('clean workspace') {
      steps {
        cleanWs()
      }
    }
    stage('checkout') {
      steps {
        checkout scm
      }
    }
    stage('AWS-Credentials') { 
        steps {
            withAWS(credentials: 'Jenkins-Terrafrom-POC-Role', region: 'us-east-1') {
            sh 'echo "it works" '
                }
            }
        }
        
    }
    stage('terraform') {
      steps {
        sh './terraformw apply -auto-approve -no-color'
      }
    }
  }
  post {
    always {
      cleanWs()
    }
  }
}
