pipeline{
    agent any
    stages{
        stage ('Build'){
            steps{
                sh 'mvn clean package'
            }
            post {
            success {
                echo 'Archiving...'
                archiveArtifacts artifacts:'**/*.war'
                }
            }
        }
        stage ('Build2'){
            steps {
                echo "Build step"
            }
        }
        stage ('Deploy'){
            steps{
                echo "Deploy"
            }
        }
    }
}