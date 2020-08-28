pipeline {
  agent any
  tools {
     maven 'M2_HOME'
  }
  stages{
    stage('Build'){
      steps{
        sh 'mvn clean'
        sh 'mvn install'
        sh 'mvn package'
      }
    }
    stage('Test'){
      steps{
        echo "test step"
        sh 'mvn test'
      }
    }
    stage('Deploy'){
      steps{
        script {
         checkout scm
         docker.withRegistry('', DockerID){
         def customImage = docker.build("femiodedina/devops-pipeline:${env.BUILD_ID}")
         customImage.push()
          }
        }
      }
    }
  }
}
