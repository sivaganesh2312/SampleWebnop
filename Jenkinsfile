pipeline {
    agent { label 'nop' }
    stages {
        stage('vcs') {
            steps {
                git branch: 'master',
                    url: 'https://github.com/sivaganesh2312/SampleWebnop.git'
            }
        }
        stage('build and analysis') {
            steps {
                withSonarQubeEnv(credentialsId: 'SONAR_CLOUD', installationName: 'sonarcloud') {
                    sh """dotnet sonarscanner begin /k:"nop-sample" /o:"august24" /d:sonar.host.url="https://sonarcloud.io"
                            dotnet build SampleMVC.sln --no-incremental
                            dotnet test SampleMVC.sln
                            dotnet publish -c Release StudentsWeb/StudentsWeb.csproj -o published/
                            dotnet sonarscanner end"""       
                }
            }
        }
    }
}