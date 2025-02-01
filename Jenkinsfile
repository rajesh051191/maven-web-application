node{
    
def mavenHome = tool name: 'Maven-3.9.9'

stage('ClonefromGIT'){
git branch: 'development', credentialsId: 'f6d6ba50-db37-47aa-9d66-e804f3a25c97', url: 'https://github.com/rajesh051191/maven-web-application.git'
}
stage('Build') {
sh "$mavenHome/bin/mvn clean package" 
}
stage("Sonarqube"){
sh "$mavenHome/bin/mvn clean sonar:sonar" 
}
stage("UploadtoNexus"){
sh "$mavenHome/bin/mvn clean deploy" 
}
stage("Tomcat_deploy"){
sshagent(['ed126ceb-e790-4a9e-8861-c66e63849853']) {
sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@13.232.64.58:/opt/apache-tomcat-9.0.98/webapps/"
}
}

}
