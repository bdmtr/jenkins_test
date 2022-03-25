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
        stage ('Deploy to staging'){
            steps{
                echo "Deploy"
                build job:'deploy_to_staging'
            }
        }
        stage ('Deploy to prod'){
            steps {
                 echo "Build step"
                 timeout(time: 5, unit:'HOURS'){
                 input message:'Approve Prod deployment?'
                 }
                 build job:'deploy_to_prod'
                 }
            }
    }
}