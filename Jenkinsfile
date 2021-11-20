pipeline {
    agent any
    parameters {
    	choice(name: 'TEST CYCLE', choices: ['SMOKE', 'REGRESSION', 'NIGHTLY'], description: '')
    }
    stages {
        stage('STATIC TESTS') {
            steps {
            	script{
                    sh 'echo Static testing...'
                    sh 'sudo python3.8 -m pylint *'
                }
            }
        }
        stage('Test') {
            steps {
                script{
                    checkout([$class: 'GitSCM', branches: [[name: 'main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/grzegorzbialobrzewski/aplikacja_kalkulator_tdd.git']]])
                    sh 'echo Testing...'
                    sh 'python3.8 -m pytest --html=report.html'
                }
                archiveArtifacts artifacts: 'report.html', followSymlinks: false
                deleteDir()
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
