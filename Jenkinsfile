pipeline {
  agent any 
  tools {
    maven 'maven' 
    jdk 'jdk11'
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
        '''
      }
    }
    stage("build") {
      steps {
        echo 'building the edm application'
        sh 'mvn clean package -Pproduction'
      }
    }
    stage("test") {
      steps {
        echo 'testing the edm application'
      }
    }
  }
}
