pipeline {
    agent any
    tools {
    jdk 'JDK21'
    maven 'Maven3'
    }
    stages {
         stage('Checkout') {
              steps {
                checkout scm
                bat 'echo Checked out branch: %BRANCH_NAME%'
              }
            }
         stage('Build') {
                     steps {

                         bat 'mvn -B clean compile'
                     }
                 }

                 stage('Test') {
                     steps {
                         // Run tests only
                         bat 'mvn -B test'
                     }
                     post {
                         always {
                             // Publish test results so Jenkins can show pass/fail
                             junit 'target/surefire-reports/*.xml'
                         }
                     }
                 }

                 stage('Package') {
                     steps {
                         // Create the JAR without running tests again
                         bat 'mvn -B package -DskipTests'
                     }
                 }

                 stage('Archive Jar') {
                     steps {
                         // Store the jar file in Jenkins
                         archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
                     }
                 }

    }

    post {
        always {
            echo "Jenkins job completed"
        }
    }
}
