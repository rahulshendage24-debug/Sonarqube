pipeline{
    agent any
    environment{
        SONAR_HOME= tool "sonar"
    }
    stages{
        stage("code"){
            steps{
                git url: "https://github.com/rahulshendage24-debug/flask-app-ecs.git" , branch: "main"
            }
        }
        stage("sonar-qube-quality-analayst"){
             steps{
                 withSonarQubeEnv("sonar"){
                     sh "$SONAR_HOME/bin/sonar-scanner -Dsonar.projectName=wanderlust -Dsonar.projectKey=wanderlust"
                 }
            }
        }
        stage("trivy file systemc scan"){
             steps{
                 sh "trivy fs --format table -o trivy-fs-report.html ."
            }
        }
        stage('deploy'){
             steps{
                 sh "docker compose up -d"
            }
        }
    }
}
