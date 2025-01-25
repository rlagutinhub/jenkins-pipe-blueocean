pipeline {
  agent any
  tool(name: 'M3', type: 'maven')
  stages {
    stage('source') {
      steps {
        git(url: 'https://github.com/jglick/simple-maven-project-with-tests.git', branch: 'master')
      }
    }

    stage('build') {
      steps {
        sh 'mvn -Dmaven.test.failure.ignore=true clean package'
      }
    }
    stage('post') {
      steps {
        junit '**/target/surefire-reports/TEST-*.xml'
        archiveArtifacts(onlyIfSuccessful: true, artifacts: 'target/*.jar\'')
      }
    }

  }
}
