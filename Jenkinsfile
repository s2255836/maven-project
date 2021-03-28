pipeline {
    agent any
    parameters{
        string(name: 'tomcat_local',defaultValue: '127.0.0.1',description: 'local example')
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
                    echo '开始存档...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

    stage ('Deployments'){
            parallel{
                stage ('Deploy to Staging'){
                    steps {
                        //sh "scp **/target/*.war ec2-user@${params.tomcat_local}:/var/lib/tomcat8/webapps"
                        sh "cp **/target/*.war /opt/tomcat/webapps"
                    }
                }
            }
        }
    }
}