pipeline {
    agent {
        label 'tomcat_app'
        {

    stages {
        stage('Checkout') {
            steps {
                git branch: 'Tomcat_App_deploy',
                    url: 'https://github.com/studymaterial9545-afk/nginx_install.git',
                    credentialsId: 'jenkinsAnsible'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                // Copy WAR file to Tomcat webapps directory on remote server
                sh '''
                scp -o StrictHostKeyChecking=no target/*.war ubuntu@13.232.95.149:/opt/tomcat/webapps/
                '''
            }
        }
    }
}
