node
{
    def mavenHome = tool name: "maven3.8.1"
    stage('GetGitHubCode')
    {
        git credentialsId: 'ed20f53b-31bc-40cb-a921-2d408757b354', url: 'https://github.com/Al-HassanTechnologies/maven-web-app.git'
    }
    stage('BuildPackage')
    {
        sh "${mavenHome}/bin/mvn clean package"
    }
    stage('ExecuteSQreport')
    {
        sh "${mavenHome}/bin/mvn sonar:sonar"
    }
    stage('DeploytoNexus')
    {
        sh "${mavenHome}/bin/mvn deploy"
    }
    stage('DeployToTomcat')
    {
        sshagent(['d2b756a6-b575-4794-b6e0-3bbbbd1a1ba7']) {
    sh "scp -o StrictHostKeyChecking=no target/maven-web-app.war ec2-user@3.109.153.250:/opt/apache-tomcat-9.0.62/webapps"
}
    }
    stage('SendEmail')
    {
        emailext body: '''Please see the logs folder attached to it


regards,
Jahangir.''', subject: 'Notification', to: 'shaikjahangir17492@gmail.com'
    }
    
    
    
    
}
