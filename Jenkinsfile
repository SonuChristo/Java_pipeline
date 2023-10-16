@Library('jenkins_shared_library') _
pipeline{
    agent any
    parameters{
        choice(name: 'action' , choices:'create\ndelete' , description:'choose create/destroy')
        string(name: 'ImageName' , description: "name of the Image" , defaultValue : 'java')
        string(name: 'ImageTag' , description: "tag of the Image" , defaultValue : 'V1')
        string(name: 'DockerHubUser' , description: "name of the application" , defaultValue : 'nathaniel2662000')
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
       stage('static code analysis : SonarQube') {
        when { expression { params.action == 'create' } }
            steps {
             script {
                 def SonarQubeCredentialsId = 'sonar-qube'
                staticCodeAnalysis(SonarQubeCredentialsId)
        }
    }
}
       stage('Quality gate status  : SonarQube') {
        when { expression { params.action == 'create' } }
            steps {
             script {
                 def SonarQubeCredentialsId = 'sonar-qube'
                qualityGateStatus(SonarQubeCredentialsId)
        }
    }
}
       stage('Maven Build : maven') {
        when { expression { params.action == 'create' } }
            steps {
             script {
                
                mavenBuild()
        }
    }
}
       stage('Docker Image : Build') {
        when { expression { params.action == 'create' } }
            steps {
             script {
                
                dockerBuild("${params.ImageName}" , "${params.ImageTag}" , "${params.DockerHubUser}")
        }
    }
}
    }
}