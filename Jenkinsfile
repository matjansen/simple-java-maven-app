pipeline {
    agent {
        docker {
            image 'maven:3-alpine'
            args '-v /root/.m2:/root/.m2'
        }
    }
    triggers {
         pollSCM('* * * * *')
    }
    stages {
         stage('Active Server') {
             steps {
                 sh 'mvn -B -DskipTests clean package'
             }
         }
         stage('Test') {
             steps {
                 sh 'mvn test'
             }
             post {
                 always {
                     junit 'target/surefire-reports/*.xml'
                 }
             }
         }
         stage('Deliver') {
             steps {
                 sh './jenkins/scripts/deliver.sh'
             }
         }
     }
}
