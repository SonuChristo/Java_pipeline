@Library('jenkins_shared_library') _
pipeline{
    agent any
    stages{
        stage('git checkout'){
            steps{
                script{
                    gitCheckout{
                        branch: "main",
                        url: "https://github.com/SonuChristo/Java_pipeline.git"
                    }
                }
            }
        }
    }
}