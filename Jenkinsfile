// 4850 Final Practical
// Agnes Ko, A01205739
// Pipeline 
pipeline {
    agent any
    parameters {
        booleanParam(defaultValue: false, description:'Run Unit Tests', name: 'TEST')
    }
    stages {
        stage('Build') {
            steps {
                echo 'Installing the Python Requirements...'
                sh 'pip install -r requirements.txt'
                echo 'Requirement complete..'
            }
        }
        
        stage('Code Quality') {
            steps {
                    sh 'pylint --fail-under=7.0 *.py'
                }
            }
        stage('Code Quantity') {
            steps {
                echo 'Student Number: A01205739'
                echo 'Group Number: 4'
                sh 'wc -l *.py'
            }
        }
        
        stage('Test') {
            when {
                expression { params.TEST }
            }
            steps {
                sh 'python3 –m unittest test_point_manager'
                }
            post {
                always {
                    junit 'test-reports/*.xml'
                }   
            }
        }
        
        stage('Package') {
            steps {
                    sh 'zip package.zip *.py'
                    archiveArtifacts artifacts: '*.zip'
            }
        }
    }
}

