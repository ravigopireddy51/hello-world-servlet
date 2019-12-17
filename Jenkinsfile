pipeline {
    agent any 
    tools { 
        maven 'Maven' 
      
    }
stages { 
     
 stage('checkout') { 
     steps {

            git 'https://github.com/ravigopireddy51/hello-world-servlet.git'

           }
   }

   stage('Build') {
       steps {  
           sh 'echo "Hello World"'
                sh '''
                    echo "Multiline shell steps works too"
                    ls -lah
                '''
            }
   }
 
  stage('Results') {
      steps {
      junit '**/target/surefire-reports/TEST-*.xml'
      archiveArtifacts 'target/*.war'
      }
 }
// stage('Sonarqube') {
//    environment {
 //       scannerHome = tool 'sonarqube'
 //   }
 //   steps {
 //       withSonarQubeEnv('sonarqube') {
 //           sh "${scannerHome}/bin/sonar-scanner"
 //       }
 //       timeout(time: 10, unit: 'MINUTES') {
 //           waitForQualityGate abortPipeline: true
 //       }
 //   }
// }
     stage('Artifact upload') {
      steps {
      nexusArtifactUploader credentialsId: '0610afd2-b5a0-4c6f-a6b5-3f84a943df32', groupId: 'com.geekcap.vmturbo', nexusUrl: 'http://15.206.127.94:8081/nexus/', nexusVersion: 'nexus2', protocol: 'http', repository: 'hello-world-servlet', version: '$BUILD_NUMBER'
      }
 }
// }
// post {
//        success {
//            mail to:"ravindrareddyg51@gmail.com", subject:"SUCCESS: ${currentBuild.fullDisplayName}", body: "Build success"
//        }
//        failure {
//            mail to:"ravindrareddyg51@gmail.com", subject:"FAILURE: ${currentBuild.fullDisplayName}", body: "Build failed"
//        }
//    }       
}
