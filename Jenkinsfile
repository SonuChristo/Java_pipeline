@Library('jenkins_shared_library') _
pipeline{
    agent any
    parameters{
        choice(name: 'action' , choices:'create\ndelete' , description:'choose create/destroy')
        string(imageName: "name of the Image" , description: "Image Name" , defaultValue : "Javaapp")
        string(imageTag: "tag of the Image" , description: "Image Tag" , defaultValue : "V1")
        string(applicationName: "name of the application" , description: "Application Name" , defaultValue : "Java")
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
                 def SonarQubeCredentialsId = 'sonar-api'
                staticCodeAnalysis(SonarQubeCredentialsId)
        }
    }
}
       stage('Quality gate status  : SonarQube') {
        when { expression { params.action == 'create' } }
            steps {
             script {
                 def SonarQubeCredentialsId = 'sonar-api'
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
                
                dockerBuild("${params.imageName} , ${params.imageTag} , ${params.applicationName}")
        }
    }
}
    }
}