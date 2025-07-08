pipeline {
    agent any
    
    environment {
        JAVA_HOME = "C:\\Program Files\\Java\\jdk-21"
        JOB_NAME = "talend-ci-cd"
    }
    
    parameters {
        string(name: 'CSV_FILE_PATH', defaultValue: 'D:/customers.csv', description: 'Path to CSV file')
    }
    
    stages {
        stage('Checkout') {
            steps {
                echo "Checking out code from GitHub..."
                checkout scm
            }
        }
        
        stage('Verify Environment') {
            steps {
                echo "Verifying Java installation..."
                bat 'java -version'
                bat 'echo JAVA_HOME: %JAVA_HOME%'
                bat 'dir'
            }
        }
        
        stage('Unzip Job') {
            steps {
                echo "Unzipping Talend job..."
                bat '''
                    if exist job2 rmdir /s /q job2
                    powershell -Command "Expand-Archive -Force CI_CD_DEMO_PROJECT_0.1.zip .\\job2"
                '''
            }
        }
        
        stage('Run Talend Job') {
            steps {
                echo "Running Talend ETL job..."
                bat '''
                    cd job2\\CI_CD_DEMO_PROJECT
                    call CI_CD_DEMO_PROJECT_run.bat --context=Default --context_param CSV_FILE_PATH=%CSV_FILE_PATH%
                '''
            }
        }
    }
    
    post {
        always {
            echo "Pipeline completed"
        }
        success {
            echo "Pipeline succeeded!"
        }
        failure {
            echo "Pipeline failed!"
        }
    }
}