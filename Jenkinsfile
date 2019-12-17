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
           sh 'mvn -Dmaven.test.failure.ignore=true install'
            }
   }
 
  stage('Results') {
      steps {
      junit '**/target/surefire-reports/TEST-*.xml'
      archiveArtifacts 'target/*.war'
      }
 }

     stage('Artifact upload') {
      steps {
     nexusPublisher nexusInstanceId: '1234', nexusRepositoryId: 'releases', packages: [[$class: 'MavenPackage', mavenAssetList: [[classifier: '', extension: '', filePath: '**/target/hello-world-servlet.war']], mavenCoordinate: [artifactId: 'hello-world-servlet-example', groupId: 'com.geekcap.vmturbo', packaging: 'war', version: '$BUILD_NUMBER']]]
      }
   }
 }
}
