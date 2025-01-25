/*
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
*/

pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "M3"
    }

    stages {
        stage('Build') {
            steps {
                // Get some code from a GitHub repository
                git 'https://github.com/jglick/simple-maven-project-with-tests.git'

                // Run Maven on a Unix agent.
                sh "mvn -Dmaven.test.failure.ignore=true clean package"

                // To run Maven on a Windows agent, use
                // bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }

            post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
                success {
                    junit '**/target/surefire-reports/TEST-*.xml'
                    archiveArtifacts 'target/*.jar'
                }
            }
        }
    }
}
