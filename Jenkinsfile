pipeline {
  agent any

  tools {
    maven 'Maven'    // name you configured in Jenkins
    jdk 'JDK17'
  }

  stages {
    stage('Checkout') {
      steps { checkout scm }
    }

    stage('Build with Maven') {
      steps {
        sh 'mvn -version'
        sh 'mvn clean package -DskipTests'
      }
    }

    stage('Deploy to Tomcat') {
      steps {
        deploy adapters: [
          tomcat9(credentialsId: 'tomcat-credentials',
                  path: '',
                  url: 'http://13.221.130.80:8080')
        ],
        contextPath: '/sample',
        war: 'target/*.war'
      }
    }
  }
}
