pipeline {
    agent { label 'nop' }
    stages {
        stage('Setup') {
            steps {
                sh 'export PATH="$PATH:$HOME/.dotnet/tools"'  // Ensure PATH includes the tool location
                sh 'dotnet tool install --global dotnet-sonarscanner || true'  // Install if not already installed
            }
        }
        stage('vcs') {
            steps {
                git branch: 'dev', url: 'https://github.com/sivaganesh2312/SampleWebnop.git'
            }
        }
        stage('build and analysis') {
            steps {
                withSonarQubeEnv('sonarcloud') {
                    sh 'dotnet sonarscanner begin /k:"nop-sample" /d:sonar.token="${SONAR_CLOUD}" /d:sonar.host.url="https://sonarcloud.io"'
                    sh 'dotnet build SampleMVC.sln --no-incremental'
                    sh 'dotnet test SampleMVC.sln'
                    sh 'dotnet publish -c Release StudentsWeb/StudentsWeb.csproj -o published/'
                    sh 'dotnet sonarscanner end /d:sonar.token="${SONAR_CLOUD}"'
                }
            }
        }
    }
}
