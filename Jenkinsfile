pipeline{
    agent any
    stages{
        stage('git checkout'){
            steps{
                script{
                    git branch: 'main', url: 'https://github.com/SonuChristo/Java_pipeline.git'
                }
            }
        }
    }
}