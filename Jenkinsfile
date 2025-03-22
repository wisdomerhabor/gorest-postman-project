pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'master', url: 'https://github.com/wisdomerhabor/gorest-postman-project.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm install -g newman newman-reporter-htmlextra'
            }
        }

        stage('Run Postman Tests') {
            steps {
                script {
                    def timestamp = new Date().format("yyyy-MM-dd_HH.mm.ss")
                    env.REPORT_NAME = "htmlextra-report-${timestamp}.html"
                }
                bat """
                mkdir "Test Results\\newman" && ^
                newman run "PROJECT 2 - FINAL COPY.postman_collection.json" --folder "E2E API AUTOMATION" ^
                -r htmlextra --reporter-htmlextra-export "Test Results\\newman\\%REPORT_NAME%" ^
                --reporter-htmlextra-title "Gorest.co.in API Test Report" ^
                --reporter-htmlextra-browserTitle "Jenkins Gorest.co.in Newman Test Report" ^
                --reporter-htmlextra-omitHeaders --reporter-htmlextra-titleSize 4 ^
                --reporter-htmlextra-darkTheme=false
                """
            }
        }

        stage('Archive Reports') {
            steps {
                archiveArtifacts "Test Results/newman/*.html"
            }
        }
    }

    post {
        always {
            publishHTML (target: [
                reportDir: 'Test Results/newman',
                reportFiles: '*.html',
                reportName: 'Newman Test Reports'
            ])
        }
    }
}
