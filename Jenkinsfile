pipeline {
    agent any

    parameters {
         string(name: 'tomcat', defaultValue: '34.228.9.186', description: 'test Server')
         }

    triggers {
         pollSCM('* * * * *')
     }

stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

        stage ('Deployments'){
              steps {
                        sh "scp /target/*.war ec2-user@${params.tomcat}:/opt/apache-tomcat-8.5.33/webapps"
                    }
                }

	}
}

