pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', url: 'https://github.com/sonupathak1/helloworld.git'
      }
    }
    stage('Pull Changes') {
      steps {
        sh 'git pull origin main'
      }
    }
    stage('Build') {
      steps {
        echo '<--------------- Building --------------->'
        sh 'printenv'
        sh 'mvn clean install'
        echo '<------------- Build completed --------------->'
      }
    }
    stage('Unit Test') {
      steps {
        echo '<--------------- Unit Testing started  --------------->'
        sh 'mvn surefire-report:report'
        echo '<------------- Unit Testing stopped  --------------->'
      }
    }
    stage("Deploy") {
          steps {
              script {
                 deploy adapters: [tomcat8(credentialsId: 'tomcat_deployer', path: '', url: 'http://192.168.56.27:9000/')], contextPath: '/pipeline', onFailure: false, war: 'webapp/target/*.war' 
              }
          }
      }

}
}
