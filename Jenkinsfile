pipeline {
    agent { label 'sonar'}
      // Make sure this is correctly defined
    
    stages {
        stage('vcs') {
            steps {
                git branch: 'master',
                    url: 'https://github.com/sivaganesh2312/SampleWebnop.git'
            }
        }
        stage('SonarQube Analysis') {
            steps {
                 
             
                withSonarQubeEnv(credentialsId: 'SONAR_CLOUD', installationName: 'sonarcloud') {
                    sh 'dotnet sonarscanner begin /k:"sivaganesh2312_SampleWebnop" /o:sivaganesh2312'
                    sh 'dotnet build SampleMVC.sln --no-incremental'
                    sh 'dotnet test SampleMVC.sln'
                    sh 'dotnet publish -c Release StudentsWeb/StudentsWeb.csproj -o published/'
                    sh 'dotnet sonarscanner end'
                    }
                }
            }
        }
    }

==================================================

