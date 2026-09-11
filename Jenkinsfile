pipeline {
agent any

triggers {
// Check GitHub every 5 minutes and build only when a new commit is found
pollSCM('H/5 * * * *')
}

environment {
GITHUB_REPOSITORY = 'https://github.com/richardbx1mai/8.2CDevSecOps.git'
STAGING_ENVIRONMENT = 'AWS EC2 Staging Server'
PRODUCTION_ENVIRONMENT = 'AWS EC2 Production Server'
}

stages {

stage('1. Build') {
steps {
echo 'Task: Fetch, compile and package the application code.'
echo 'Build automation tool: npm'

git branch: 'main',
url: "${GITHUB_REPOSITORY}"

echo 'Command that could be used: npm install'
echo 'Command that could be used: npm run build'
}
}

stage('2. Unit and Integration Tests') {
steps {
echo 'Task: Run unit tests to verify individual functions and components.'
echo 'Task: Run integration tests to verify that application components work together.'
echo 'Test automation tools: Mocha and npm test'
echo 'Command that could be used: npm test'
}
}

stage('3. Code Analysis') {
steps {
echo 'Task: Analyse the source code for bugs, code smells and maintainability issues.'
echo 'Code analysis tool: SonarCloud using SonarScanner'
echo 'Command that could be used: sonar-scanner'
}
}

stage('4. Security Scan') {
steps {
echo 'Task: Scan application dependencies for known security vulnerabilities.'
echo 'Security scanning tool: npm audit'
echo 'Command that could be used: npm audit'
}
}

stage('5. Deploy to Staging') {
steps {
echo "Task: Deploy the application to ${STAGING_ENVIRONMENT}."
echo 'Deployment tool: AWS CLI'
echo 'Example deployment method: Package and copy the application to an AWS EC2 staging instance.'
}
}

stage('6. Integration Tests on Staging') {
steps {
echo "Task: Run integration tests against ${STAGING_ENVIRONMENT}."
echo 'Integration testing tool: Postman with Newman'
echo 'Command that could be used: newman run staging-tests.postman_collection.json'
}
}

stage('7. Deploy to Production') {
steps {
echo "Task: Deploy the tested application to ${PRODUCTION_ENVIRONMENT}."
echo 'Deployment tool: AWS CLI'
echo 'Example deployment method: Package and copy the approved application to an AWS EC2 production instance.'
}
}
}

post {
success {
echo 'All seven pipeline stages completed successfully.'
}

failure {
echo 'The pipeline failed. Review the Jenkins console output.'
}

always {
echo 'Pipeline execution has finished.'
}
}
}