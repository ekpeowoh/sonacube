pipeline {
  agent any
  tools {
    maven 'maven'
  }
  stages{
    stage('1-git-clone'){
      steps{
        checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'b48b6025-4625-4037-8d4b-f7c12674d945', url: 'https://github.com/ekpeowoh/sonacube.git']])
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
       sh 'mvn clean verify sonar:sonar \
  -Dsonar.projectKey=team5codereview \
  -Dsonar.projectName='team5codereview' \
  -Dsonar.host.url=http://ec2-52-91-245-107.compute-1.amazonaws.com:9000 \
  -Dsonar.token=sqp_3f56a6b940ee3d2e7c10d9964a6c2bcf8113cab0'
        }
    }
  }
}
