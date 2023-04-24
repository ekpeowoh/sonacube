pipeline {
  agent any
  tools {
    maven 'maven'
  }
  stages{
    stage('1-git-clone'){
      steps{
        checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'github-id', url: 'https://github.com/etechDevops/etech-mavenApp.git']]])
      }
    }
    stage('2-cleanws'){
      steps{
        sh 'mvn clean'
      }
    }
    stage('3-mavenbuild'){
      steps{
        sh 'mvn package'
      }
    }
    stage('unittest'){
        steps{
            sh 'mvn test'
        }
    }
    stage('codequality'){
        steps{
       sh "mvn clean verify sonar:sonar \
  -Dsonar.projectKey=team5codereview2 \
  -Dsonar.projectName='team5codereview2' \
  -Dsonar.host.url=http://ec2-44-206-224-80.compute-1.amazonaws.com:9000 \
  -Dsonar.token=sqp_87d7fca481b1159a6079ba2167745818547f8945"
        }
    }
  }
}
