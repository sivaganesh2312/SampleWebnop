pipeline {
    agent any
    stages {
        stage('vcs') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/dummyrepos/SampleWeb.git'
            }
        }
        stage('build') {
            steps {
                sh 'dotnet build SampleMVC.sln'
                sh 'dotnet test SampleMVC.sln'
                sh 'dotnet publish -c Release StudentsWeb/StudentsWeb.csproj -o published/'
                zip zipFile: 'samplemvc.zip',
                      archive: true,
                      dir: './published',
                      overwrite: true
                sh 'rm -rf ./published'
            }
        }
    }
}