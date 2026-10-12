pipeline {
   agent any

   tools {
      maven 'MAVEN_HOME'
   }

   stages {
      stage('git repo & clean') {
         steps {
            bat 'if exist maven-main rmdir /s /q maven-main'
            bat 'git clone https://github.com/Miteshreddy/doc_Maven.git maven-main'
            bat 'mvn clean -f maven-main/pom.xml'
         }
      }

      stage('install') {
         steps {
            bat 'mvn install -f maven-main/pom.xml'
         }
      }

      stage('test') {
         steps {
            bat 'mvn test -f maven-main/pom.xml'
         }
      }

      stage('package') {
         steps {
            bat 'mvn package -f maven-main/pom.xml'
         }
      }
   }

   post {
      success {
         emailext(
            to: 'miteshguduru@gmail.com',
            from: 'miteshguduru@gmail.com',
            replyTo: 'miteshguduru@gmail.com',
            subject: "SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
            body: """The Jenkins pipeline completed successfully.

Job: ${env.JOB_NAME}
Build Number: ${env.BUILD_NUMBER}
Build URL: ${env.BUILD_URL}

All pipeline stages completed successfully."""
         )
      }
      failure {
         emailext(
            to: 'miteshguduru@gmail.com',
            from: 'miteshguduru@gmail.com',
            replyTo: 'miteshguduru@gmail.com',
            subject: "FAILURE: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
            body: """The Jenkins pipeline failed.

Job: ${env.JOB_NAME}
Build Number: ${env.BUILD_NUMBER}
Build URL: ${env.BUILD_URL}

Please check the Jenkins Console Output for details."""
         )
      }
   }
}
