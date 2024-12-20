pipeline {
    agent any

    environment {
        SONARQUBE_URL = 'http://localhost:9000'
        SONARQUBE_TOKEN = credentials('sonarqube-token') // Utiliser le token enregistré dans Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                // Récupérer le code source du dépôt Git
                checkout scm
            }
        }

        stage('Build') {
            steps {
                // Construire le projet (par exemple avec Maven ou Gradle)
                script {
                    // Exemple pour Maven
                    sh 'mvn clean install'

                    // Si vous utilisez Gradle, vous pouvez remplacer par :
                    // sh './gradlew build'
                }
            }
        }

        stage('SonarQube Analysis') {
            steps {
                // Analyser le projet avec SonarQube
                script {
                    // Vérifier que SonarScanner est bien installé dans Jenkins
                    sh '''
                    sonar-scanner \
                    -Dsonar.projectKey=Gestion_Biblio \
                    -Dsonar.sources=src \
                    -Dsonar.host.url=$SONARQUBE_URL \
                    -Dsonar.login=$SONARQUBE_TOKEN
                    '''
                }
            }
        }

        stage('Test') {
            steps {
                // Exécuter les tests unitaires
                script {
                    // Exemple pour Maven
                    sh 'mvn test'

                    // Si vous utilisez Gradle, vous pouvez remplacer par :
                    // sh './gradlew test'
                }
            }
        }

        stage('Deploy') {
            steps {
                // Déployer l'application (si nécessaire)
                sh 'scp target/monapp.jar user@serveur:/chemin/deploiement'
            }
        }
    }

    post {
        success {
            echo 'Le build, l\'analyse et les tests ont réussi.'
        }
        failure {
            echo 'Le build ou l\'analyse SonarQube a échoué.'
        }
    }
}
