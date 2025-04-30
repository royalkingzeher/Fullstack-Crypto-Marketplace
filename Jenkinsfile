pipeline {
    agent any

    tools {
        maven 'MAVEN_HOME' 
    }

    stages {

        stage('Stage 1: Clean Workspace') {
            steps {
                echo 'Running mvn clean...'
                sh 'mvn clean'
            }
        }

        stage('Stage 2: Compile Code') {
            steps {
                echo 'Running mvn compile...'
                sh 'mvn compile'
            }
        }

        stage('Stage 3: Run Tests') {
            steps {
                echo 'Running mvn test...'
                sh 'mvn test'
            }
        }

        stage('Stage 4: Package Application') {
            steps {
                echo 'Running mvn package...'
                sh 'mvn package'
            }
        }

        stage('Stage 5: Install Artifacts') {
            steps {
                echo 'Running mvn install...'
                sh 'mvn install'
            }
        }

        stage('Stage 6: Static Code Analysis') {
            steps {
                echo 'Running static code analysis (e.g., SpotBugs or SonarQube)...'
            }
        }

        stage('Stage 7: Archive Artifacts') {
            steps {
                echo 'Archiving JAR/WAR file...'
                archiveArtifacts artifacts: "${BUILD_DIR}/*.jar", allowEmptyArchive: true
            }
        }

        stage('Stage 8: Deploy to Staging') {
            steps {
                echo 'Deploying to staging environment'
            }
        }

        stage('Stage 9: Manual Approval for Production') {
            when {
                branch 'main'
            }
            steps {
                input message: 'Approve deployment to production?'
            }
        }

        stage('Stage 10: Deploy to Production') {
            when {
                branch 'main'
            }
            steps {
                echo 'Deploying to production environment...'
                // sh './deploy.sh production'
            }
        }

        stage('Final Stage: Build Complete') {
            steps {
                echo 'Build & Deployment Pipeline Completed Successfully!'
            }
        }
    }

    post {
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed.'
        }
        always {
            echo 'Cleaning up...'
            cleanWs()
        }
    }
}
