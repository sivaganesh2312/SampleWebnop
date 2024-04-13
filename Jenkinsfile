pipeline {
    agent any
    stages {
        stage('vcs') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/dummyrepos/SampleWeb.git'
            }
        }
        stage('build and analysis') {
            steps {
                withSonarQubeEnv(credentialsId: 'SONAR_CLOUD', installationName: 'sonarcloud') {
                    sh 'dotnet sonarscanner begin /k:"april24_sampleweb" /o:april24'
                    sh 'dotnet build SampleMVC.sln --no-incremental'
                    sh 'dotnet test SampleMVC.sln'
                    sh 'dotnet publish -c Release StudentsWeb/StudentsWeb.csproj -o published/'
                    sh 'dotnet sonarscanner end'
                    
                }
                
            }
        }
        stage("Quality Gate") {
            steps {
                timeout(time: 1, unit: 'HOURS') {
                    // Parameter indicates whether to set pipeline to UNSTABLE if Quality Gate fails
                    // true = set pipeline to UNSTABLE, false = don't
                    waitForQualityGate abortPipeline: true
                }
            }
        }
        
    }
}