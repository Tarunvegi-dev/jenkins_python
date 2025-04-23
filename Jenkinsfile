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
                # First try standard venv
                python3.11 -m venv venv || {
                    echo "Standard venv failed, trying alternative approach"
                    # Fallback 1: Use ensurepip bootstrap
                    python3.11 -m ensurepip --user || true
                    python3.11 -m venv --without-pip venv
                    curl -sS https://bootstrap.pypa.io/get-pip.py | venv/bin/python
                }
                # Install requirements
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
