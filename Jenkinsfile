pipeline {
    triggers {
  pollSCM('* * * * *')
    }
   agent any
    tools {
  maven 'M2_HOME'
}
environment {
    registry = '076892551558.dkr.ecr.us-east-1.amazonaws.com/jenkins'
    registryCredential = 'jenkins-ecr'
    dockerimage = ''

     NEXUS_VERSION = "nexus3"
     NEXUS_PROTOCOL = "http"
     NEXUS_URL = "139.177.192.139:8081"
     NEXUS_REPOSITORY = "utrains-nexus-pipeline"
     NEXUS_CREDENTIAL_ID = "nexus-user-credentials"
     POM_VERSION = ''
}
    stages {

        stage('maven package') {
            steps {
                dir('./backend_digital_banking_secure/'){
                    sh 'mvn clean'
                    sh 'mvn package -DskipTests'
                }
            }
        }
        stage('Build Image') {
            
            steps {
                dir('./backend_digital_banking_secure/'){
                     script{
                        def mavenPom = readMavenPom file: 'pom.xml'
                        POM_VERSION = "${mavenPom.version}"
                        echo "${POM_VERSION}"
                        dockerImage = docker.build registry + ":${POM_VERSION}"
                    } 

                }
            }
        }
 	    
    }
}