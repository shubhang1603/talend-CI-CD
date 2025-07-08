pipeline {
    agent any
    environment {
        JAVA_HOME = "C:\\Program Files\\Java\\jdk-21"
        TALEND_CLI = "C:\\studio\\Talend-Studio-win-x86_64"
        JOB_NAME = "talendcicd_0.1"
    }
    parameters {
        string(name: 'CSV_FILE_PATH', defaultValue: 'C:/studio/talend-ci-cd/customers.csv')
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/shubhang1603/talend-CI-CD.git'
            }
        }
        stage('Unzip Job') {
            steps {
                bat '''powershell -Command "Expand-Archive -Force talendcicd_0.1.zip .\\job2"'''
            }
        }
        stage('Run Talend Job') {
            steps {
                bat '''
cd job2\\talendcicd
call talendcicd_run.bat --context=Default ^
--context_param CSV_FILE_PATH=%CSV_FILE_PATH%
'''
            }
        }
    }
}
