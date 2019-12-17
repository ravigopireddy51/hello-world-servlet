pipeline {
    agent any 
    tools { 
        maven 'Maven' 
   }
stages { 
     
 stage('checkout') { 
     steps {
           checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'jenkins', url: 'https://github.com/ravigopireddy51/hello-world-servlet.git']]])

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
      archiveArtifacts 'target/*.jar'
      }
 }
stage('Sonarqube') {
    environment {
       scannerHome = tool 'sonarqube'
    }
    steps {
        withSonarQubeEnv('sonarqube') {
            sh "${scannerHome}/bin/sonar-scanner"
        }
        timeout(time: 02, unit: 'MINUTES') {
            waitForQualityGate abortPipeline: true
        }
    }
 }
     stage('Artifact upload') {
      steps {
     nexusPublisher nexusInstanceId: '1234', nexusRepositoryId: 'releases', packages: [[$class: 'MavenPackage', mavenAssetList: [[classifier: '', extension: '', filePath: '**/target/hello-world-servlet.war']], mavenCoordinate: [artifactId: 'hello-world-servlet-example', groupId: 'com.geekcap.vmturbo', packaging: 'war', version: '$BUILD_NUMBER']]]
      }
   }
 }
}
