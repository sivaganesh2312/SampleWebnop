pipeline {
    agent { label 'nop' }
    stages {
        stage('vcs') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/dummyrepos/SampleWeb.git'
            }
        }
        stage('build and analysis') {
            steps {
                    sh 'dotnet build SampleMVC.sln --no-incremental'
                    sh 'dotnet test SampleMVC.sln'
                    sh 'dotnet publish -c Release StudentsWeb/StudentsWeb.csproj -o published/'
                    
                
                
            }
        }
    }
}