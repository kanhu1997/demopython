pipeline {
    agent any

    environment {
        VENV_DIR = "venv"
    }

    stages {
        stage('Notify for Approval') {
            steps {
                mail to: 'kanhucharandash55@gmail.com',
                     subject: 'Approval Needed for Python App Deployment',
                     body: 'A Jenkins job requires your approval. Please go to Jenkins and approve it in the pipeline UI.'
            }
        }

        stage('Wait for Manual Approval') {
            steps {
                input message: 'Do you approve deploying the Flask app?', ok: 'Yes, Deploy'
            }
        }

        stage('Set up virtual environment') {
            steps {
                sh '''
                    python3 -m venv ${VENV_DIR}
                    . ${VENV_DIR}/bin/activate
                    pip install --upgrade pip
                    pip install -r requirements.txt
                '''
            }
        }

        stage('Run Flask App') {
            steps {
                sh '''
                    . ${VENV_DIR}/bin/activate
                    export FLASK_APP=app.py
                    export FLASK_ENV=development
                    flask run --host=localhost --port=5000 &
                '''
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished.'
        }
    }
}
