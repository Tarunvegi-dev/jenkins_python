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
        stage('Setup') {
            steps {
                sh '''
                # Ensure python3.11-venv is available (if system allows)
                python3.11 -m ensurepip --default-pip || true
                '''
            }
        }
        stage('Build') {
            steps {
                sh '''
                cd myapp
                # Create fresh venv (forcing pip inclusion)
                python3.11 -m venv --clear --upgrade-deps venv
                # Use direct path to avoid activation issues
                venv/bin/pip install --no-cache-dir -r requirements.txt
                '''
            }
        }
        stage('Test') {
            steps {
                sh '''
                cd myapp
                # Use venv's python directly
                venv/bin/python hello.py
                venv/bin/python hello.py --name=TarunVegi
                '''
            }
        }
    }
}
