pipeline {
    agent any

    stages {
        stage('Construction de l\'image Docker') {
            steps {
                sh 'docker build -t ma-super-image-github:1.0 .'
                echo 'L\'image a été construite avec succès !'
            }
        }
        stage('Vérification') {
            steps {
                sh 'docker images ma-super-image-github'
            }
        }
    }
}wall
