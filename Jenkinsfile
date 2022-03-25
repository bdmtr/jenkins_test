pipeline{
    agent any
    triggers {
        pollSCM('*/5 * * * *')
    }
    stages{
        stage ('Build'){
            steps {
                sh 'mvn clean package'
            }
            post {
            success {
                echo 'Archiving...'
                archiveArtifacts artifacts:'**/*.war'
                }
            }
        }
        stage ('Deployments'){
            parallel {
                stage ('Deploy to staging...'){
                    steps {
                        echo "Deploy"
                        sh "cp **/target/*.war /home/userman/programms/tomcat"
                        }
                    }
                    stage ('Deploy to prod...'){
                    steps {
                        echo "Build step..."
                        sh "cp **/target/*.war /home/userman/programms/tomcat-prod"
                    }
                }
            }
        }
    }
    }
