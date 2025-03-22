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
                sh 'npm install -g newman newman-reporter-htmlextra'
            }
        }

        stage('Run Postman Tests') {
            steps {
                sh '''
                newman run "PROJECT 2 - FINAL COPY.postman_collection.json" \
                -d "Test Data/createUserAPI-DDT.csv" \
                -r htmlextra --reporter-htmlextra-title "Gorest API Test Report" \
                --reporter-htmlextra-browserTitle "Jenkins Newman Test Report" \
                --reporter-htmlextra-omitHeaders --reporter-htmlextra-titleSize 4 \
                --reporter-htmlextra-darkTheme=false
                '''
            }
        }

        stage('Archive Reports') {
            steps {
                archiveArtifacts 'newman/*.html'
            }
        }
    }
}
