pipeline {
  agent any 
  stages {
    stage("Configure") {
      steps {
        echo 'setting up environment config'
         sh '''
            echo "PATH = ${PATH}"
            echo "M2_HOME = ${M2_HOME}"
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
