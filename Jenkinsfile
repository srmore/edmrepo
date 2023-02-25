pipeline {
  agent any 
  tools {
    maven 'maven' 
    jdk 'jdk11'
    docker 'docker'
  }
  stages {
    stage("Configure") {
      steps {
        echo 'setting up environment config'
         sh '''
            echo "PATH = ${PATH}"
            echo "JAVA_HOME = ${JAVA_HOME}"
            echo "M2_HOME = ${M2_HOME}"
            java -version
            docker --version
        '''
      }
    }
    stage("build") {
      steps {
        echo 'building the edm application'
        sh 'mvn clean install'
      }
    }
    stage("test") {
      steps {
        echo 'testing the edm application'
      }
    }
    stage("build image") {
      steps {
        echo 'building docker image'
        sh 'docker build -t edm:1.0 .'
      }
    }
  }
}
