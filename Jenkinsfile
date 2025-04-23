pipeline {
    agent { 
        node {
            label 'docker-agent-python'
        }
    }
    triggers {
        pollSCM '* * * * *'
    }
    stages {
        stage('Build') {
            steps {
                echo "Building.."
                sh '''
                cd myapp
                python3 -m venv --without-pip venv
                # Use dot notation instead of source for better compatibility
                . venv/bin/activate
                pip install --no-cache-dir -r requirements.txt
                '''
            }
        }
        stage('Test') {
            steps {
                echo "Testing.."
                sh '''
                cd myapp
                # Explicitly use the virtual environment's Python
                myenv/bin/python hello.py
                myenv/bin/python hello.py --name=TarunVegi
                '''
            }
        }
        stage('Deliver') {
            steps {
                echo 'Deliver....'
                sh '''
                echo "doing delivery stuff.."
                '''
            }
        }
    }
}
