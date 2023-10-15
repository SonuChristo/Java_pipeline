@Library('jenkins_shared_library') _
pipeline{
    agent any
    stages{
        stage('Git Checkout'){
            steps{
            gitCheckout(
                        branch: "main",
                        url: "https://github.com/SonuChristo/Java_pipeline.git"
            )    
            }
        }
        stage('Unit Testing Using Maven'){
            steps{
                scripts{
                    mvnTest()
                }
            }
        }
    }
}