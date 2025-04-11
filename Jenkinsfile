pipeline {
 agent any
 
 environment {
 FLASK_APP = 'app.py'
 FLASK_ENV = 'development'
 }
 
 stages {
 stage('Build') {
 steps {
 script {
 echo 'Building Python Flask app...'
 sh 'pip install -r requirements.txt'
 }
 }
 }
 stage('Test') {
 steps {
 script {
 echo 'Running tests...'
 // Add any test commands here if needed
 }
 }
 }

 stage('Approve via email') {
 steps {
 emailext to: 'kanhucharandash@gmail.com', mimeType: 'text/html', subject: 'New build is waiting for your approval', body: '<html><p>A new build has been deployed, please view it by visiting <a href=http://localhost:8000/>"http://localhost:8080/"</a>, please approve this deployment by clicking on <a href=http://localhost:8080/job/demopyapp/${BUILD_NUMBER}/input/>"http://localhost:8080/${BUILD_NUMBER}/input/"</a></p></html>', attachLog: true
 timeout(time: 60, unit: 'MINUTES') {
 }
 }
 }
  
 stage('Approval') {
 steps {
 timeout(time: 24, unit: 'HOURS') {
 input message: 'Do you approve the deployment?', submitter: 'admin'
 }
 }
 }

 stage('Deploy') {
 steps {
 script {
 echo 'Deploying Python Flask app...'
 sh 'python app.py'
 }
 }
 }
 }
 
 post {
 success {
 echo 'Pipeline succeeded!'
 }
 failure {
 echo 'Pipeline failed!'
 }
 }
}
