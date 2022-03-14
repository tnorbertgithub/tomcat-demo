node {
    def mvnHome = tool name: 'maven home', type: 'maven'
    stage('SCM-Checkout') {
        git branch: 'main', credentialsId: 'Git-Credentials', url: 'https://github.com/tnorbertgithub/tomcat-demo.git'
    }
    stage('mvn-clean') {
        sh "${mvnHome}/bin/mvn clean"
    }
    stage('mvn-compile') {
        sh "${mvnHome}/bin/mvn compile"
    }
    stage('mvn-test') {
        sh "${mvnHome}/bin/mvn test"
    }
    stage('mvn-package') {
        sh "${mvnHome}/bin/mvn package"
    }
    stage('Tomcat Deployment') { 
        sshagent(['ec2-user']) {
    sh 'sudo scp -o StrictHostKeyChecking=no target/tomcat-demo.war root@172.31.29.134:/opt/tomcat/webapps/'
    }
    }
}
