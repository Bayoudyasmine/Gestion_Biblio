pipeline {
    agent any
    environment {
        SONARQUBE = 'http://localhost:9000'  // L'adresse de votre serveur SonarQube
        SONAR_TOKEN = 'squ_6d1a095cccb54760f3ebe7d3daa13c532892b38e'     // Le token d'authentification pour SonarQube
    }
    stages {
        stage('Checkout') {
            steps {
                // Récupérer le code depuis GitHub
                git 'https://github.com/Bayoudyasmine/Gestion_Biblio.git'
            }
        }
        stage('SonarQube Analysis') {
            steps {
                // Exécuter l'analyse SonarQube avec Maven ou le Scanner
                withSonarQubeEnv('SonarQube') {
                    sh 'mvn clean install sonar:sonar -Dsonar.projectKey=Gestion_Biblio'  // Utiliser le scanner si vous ne travaillez pas avec Maven
                }
            }
        }
      stage('SonarQube Analysis') {
          steps {
              withSonarQubeEnv('SonarQube') {
                  sh 'mvn clean install sonar:sonar -Dsonar.projectKey=Gestion_Biblio'
                  echo 'SonarQube analysis has been triggered.'
              }
          }
      }

    }
}
