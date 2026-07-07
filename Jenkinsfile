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
                script {
                    clone("https://github.com/nishnischal/django-notes-app.git", "main")
                    echo "Code cloning successful"
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    docker_build("notes-app", "latest")
                }
            }
        }

        stage('Push') {
            steps {
                script {
                    docker_push("notes-app", "latest", "nischalojha")
                }
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying application..."
                sh "docker compose down && docker compose up -d"
            }
        }
    }
}
