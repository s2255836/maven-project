pipeline {
    agent any
    tools{
        maven 'local_MVN'
    }
    stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo '开始...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage('deploy_local'){
            steps{
                timeout(time:5, unit: 'DAYS'){
                    input message: '部署嗎？？？'
                }
                build job: 'deploy-to-local'
            }
            post {
                success {
                    echo '部署囉～～～'
                }

                failure {
                    echo '失敗囉～～'
                }
            }
        }
    }
}
