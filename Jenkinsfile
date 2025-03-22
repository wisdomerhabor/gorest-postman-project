pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/wisdomerhabor/gorest-postman-project.git'
            }
        }

        stage('Install Newman') {
            steps {
                bat 'npm install -g newman newman-reporter-htmlextra'
            }
        }

        stage('Run Postman Tests') {
            steps {
                bat '''
                cd %WORKSPACE%
                C:\Users\Wisdom.Erhabho\.jenkins\workspace\gorest-postman-project>newman run "PROJECT 2 - FINAL COPY.postman_collection.json" --folder "E2E API AUTOMATION" -r htmlextra --reporter-htmlextra-title "Gorest.co.in API Test Report" --reporter-htmlextra-browserTitle "Jenkins Gorest.co.in Newman Test Report" --reporter-htmlextra-omitHeaders --reporter-htmlextra-titleSize 4 --reporter-htmlextra-darkTheme=false
                '''
            }
        }

        stage('Archive Reports') {
            steps {
                archiveArtifacts 'newman/*.html'
            }
        }
    }

    post {
        always {
            publishHTML (target: [
                reportDir: 'newman',
                reportFiles: 'jenkins-htmlextra-report.html',
                reportName: 'Jenkins Newman Test Report'
            ])
        }
    }
}
