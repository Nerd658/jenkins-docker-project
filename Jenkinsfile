pipeline {
    agent any

    environment {
        // On définit des variables pour ne pas avoir à les répéter
        DOCKERHUB_CREDENTIALS_ID = 'dockerhub-credentials'
        DOCKERHUB_USERNAME = 'hassan1118' // 
        IMAGE_NAME = 'ma-super-image'
    }

    stages {
        stage('Construction de l\'image Docker') {
            steps {
                // On ajoute un tag "latest" dès la construction
                sh "docker build -t ${DOCKERHUB_USERNAME}/${IMAGE_NAME}:latest ."
            }
        }
        stage('Push to Docker Hub') {
            steps {
                // On utilise le coffre-fort de Jenkins pour se connecter
                withCredentials([usernamePassword(credentialsId: DOCKERHUB_CREDENTIALS_ID, usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    echo 'Connexion à Docker Hub...'
                    sh "echo ${PASS} | docker login -u ${USER} --password-stdin"
                    
                    echo 'Publication de l\'image...'
                    sh "docker push ${DOCKERHUB_USERNAME}/${IMAGE_NAME}:latest"
                }
            }
        }
        stage('Nettoyage') {
            steps {
                // C'est une bonne pratique de nettoyer l'image de la machine locale après le push
                echo 'Nettoyage de l\'image locale...'
                sh "docker rmi ${DOCKERHUB_USERNAME}/${IMAGE_NAME}:latest"
            }
        }
    }
}
