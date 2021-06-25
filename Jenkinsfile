pipeline{
    agent any
    stages{
        stage("clone git code"){
            steps{
                git branch: 'master', credentialsId: 'git_credentials', url: 'https://github.com/kkarun-ges/sample-java-app.git'
            }
        }
        stage("build code"){
            steps{
                sh "mvn clean package"
            }
        }
        stage("deploy code to tomcat server"){
            steps{
                sshagent(['deploy-user']) {
                    sh 'scp -o StrictHostKeyChecking=no target/spring-boot-rest-example-0.5.0.war ubuntu@ec2-34-210-36-110.us-west-2.compute.amazonaws.com:/opt/tomcat/apache-tomcat-8.5.68/webapps'
                }
            }
        }
    }
}
