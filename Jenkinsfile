pipeline {
    agent { 
        node {
            label 'docker-agent-python'
        }
    }
    triggers {
        pollSCM '* * * * *'  // Keeping your original trigger
    }
    stages {
        stage('Build') {
            steps {
                echo "Building.."
                sh '''
                cd myapp
                # Fallback solution that works without system packages
                python3.11 -m pip install --user virtualenv
                python3.11 -m virtualenv venv
                venv/bin/pip install --no-cache-dir -r requirements.txt
                '''
            }
        }
        stage('Test') {
            steps {
                echo "Testing.."
                sh '''
                cd myapp
                venv/bin/python hello.py
                venv/bin/python hello.py --name=TarunVegi
                '''
            }
        }
        stage('Deliver') {
            steps {
                echo 'Deliver....'
                sh '''
                echo "Performing delivery operations..."
                '''
            }
        }
    }
}
