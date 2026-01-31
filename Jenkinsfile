pipeline {
    agent any

    tools {
        maven 'local_maven'
    }
    parameters {
        string(name:'staging-server', defaulValue: '13.232.246.51', description: 'Remote tomcat server')
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    archiveartifacts artifacts: '**/*.war'
                }
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                // Copy WAR file to Tomcat webapps directory on remote server
                sh '''
                scp -v -o StrictHostKeyChecking=no **/*.war root@13.232.246.51:/home/ubuntu/tomcat10/webapps/
                '''
            }
        }
    }
}

