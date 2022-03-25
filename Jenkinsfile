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
                        sh "cp **/target/*.war /opt/tomcat/webapps"
                        }
                    }
                    stage ('Deploy to prod...'){
                    steps {
                        echo "Build step..."
                        sh "cp **/target/*.war /opt/tomcat-prod/webapps"
                    }
                }
            }
        }
    }
    }
