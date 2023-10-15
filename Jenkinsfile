@Library('jenkins_shared_library') _
pipeline{
    agent any
    parameters{
        choice(name: 'action' , choices:'create\ndelete' , description:'choose create/destroy')
    }
    stages{
        
        stage('Git Checkout'){
            when { expression{ params.action == 'create'}}
            steps{
            gitCheckout(
                        branch: "main",
                        url: "https://github.com/SonuChristo/Java_pipeline.git"
            )    
            }
        }
        
        stage('Unit Testing Using Maven'){
            when {expression { params.action == 'create'}}
            steps{
                script{
                    mvnTest()
                }
            
            }
        }
       
        stage('Integration Mvn test'){
            when{ expression { params.action== 'create'}}
            steps{
                script{
                    mvnIntegrationTest()
                }
            
            }
        }
        stage('static code analysis : SonarQube'){
            when{ expression { params.action== 'create'}}
            steps{
                script{
                    def SonarQubeCredentialsId = 'sonarqube-api'
                    staticCodeAnalysis(SonarQubeCredentialsId)
                }
            
            }
        }
    }
}