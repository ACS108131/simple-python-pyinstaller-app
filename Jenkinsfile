def username='123'
pipeline {
    agent any 
    
    stages {
        stage('Build') { 
            steps {
                bat 'python -m py_compile sources/add2vals.py sources/calc.py' 
                bat "echo '${username}'"
            }
        }
        stage('Test') {
            steps {
                bat 'pytest --verbose --junit-xml test-reports/results.xml sources/test_calc.py'
            }
            post {
                always {
                    junit 'test-reports/results.xml'

                }
            }
        }
        stage('Deliver') {
            steps {
                bat 'pyinstaller --onefile sources/add2vals.py'
                
            }
            post {
                success {
                    archiveArtifacts 'dist/add2vals.exe'
                    
                    
                }
            }
        }
    }
}