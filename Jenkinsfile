@Library("shared") _
pipeline {
    agent { label "hamza" }

    stages {
        stage("Hello"){
            steps{ 
                script{
                    hello()
                }
            }
        }

        stage("Clean Workspace") {
            steps {
                cleanWs()
            }
        }

        stage("Code") {
            steps {
                echo "Cloning code"
                git url: "https://github.com/nishnischal/django-notes-app.git", branch: "main"
            }
        }

        stage("Build") {
            steps {
                script{
                    docker_build("notes-app","latest", "nischalojha")
                }
            }
        }
        stage("Push to DockerHub") {
                steps{
                    script{
                        docker_push("notes-app","latest","nischalojha")
                    }
                }
                }
        stage("Test") {
            steps {
                echo "Running tests"
            }
        }

        stage("Deploy") {
            steps {
                echo "Deploying app"
                sh '''
                docker compose down &&
                docker compose up -d
                '''
            }
        }
    }

    post {
        always {
            echo "Cleaning unused Docker resources"
            sh "docker system prune -f"
        }
    }
}
