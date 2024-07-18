pipeline {
    agent any
    parameters {
        choice choices: ['chrome', 'firefox'], description: 'Select the browser to run the test', name: 'BROWSER'
    }
    stages {
        stage('Start Grid') {
            steps {
                sh "docker-compose -f grid.yml up --scale ${params.BROWSER}=2 -d"
            }
        }
        stage('Run Tests') {
            steps {
                sh "docker-compose -f test-suites.yml up"
            }
        }
    }
    post {
        always {
            sh "docker-compose -f grid.yml down"
            sh "docker-compose -f test-suites.yml down"
            archiveArtifacts artifacts: 'output/flight-reservation/emailable-report.html', followSymlinks: false
            archiveArtifacts artifacts: 'output/vendor-portal/emailable-report.html', followSymlinks: false
        }
    }
}
