@Library("Shared") _

pipeline {
    agent { label "vinod" }

    stages {

        stage('Hello') {
            steps {
                script {
                    hello()
                }
            }
        }

        stage('Code') {
            steps {
                echo "Fetching code from GitHub..."

                git branch: "main",
                    url: "https://github.com/nishnischal/django-notes-app.git"

                echo "Code cloning successful"
            }
        }

        stage('Build') {
            steps {
                echo "Building Docker image..."

                sh "docker build -t notes-app:latest ."
            }
        }

        stage('Test') {
            steps {
                echo "Testing the application..."
                // sh "python manage.py test"
            }
        }

        stage('Push') {
            steps {
               script {
                  docker_push("notes-app","latest","nischalojha")
              }
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying application..."
                sh "docker compose up -d"
                
            }
        }
    }
}
