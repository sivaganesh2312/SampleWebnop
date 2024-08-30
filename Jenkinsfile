pipeline {
    agent { label 'nop' }
    stages {
        stage('vcs') {
            steps {
                git branch: 'dev',
                    url: 'https://github.com/sivaganesh2312/SampleWebnop.git'
            }
        }
        stage('build and analysis') {
            steps {
                withSonarQubeEnv(credentialsId: 'SONAR_CLOUD', installationName: 'sonarcloud') {
                  sh 'dotnet tool install --global dotnet-sonarscanner || exit 0'
                  sh 'dotnet sonarscanner begin /k:"nop-sample" /d:sonar.token="$SONAR_CLOUD" /d:sonar.host.url="https://sonarcloud.io"'
                  sh 'dotnet build SampleMVC.sln --no-incremental'
                  sh 'dotnet sonarscanner end /d:sonar.token="$SONAR_CLOUD"'     
                }
            }
        }
    }
}