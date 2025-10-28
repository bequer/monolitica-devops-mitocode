pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                echo 'Compilando proyecto Java con Maven...'
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Testing') {
            steps {
                echo 'Ejecutando pruebas unitarias con JUnit...'
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }

        stage('Analisis SonarQube') {
            steps {
                echo 'Analizando calidad de código en SonarQube...'
                withSonarQubeEnv('SonarQube') {
                    sh 'mvn sonar:sonar'
                }
            }
        }

        stage('Publicar Artefacto en Artifactory') {
            steps {
                echo 'Subiendo el artefacto generado al repositorio Artifactory...'
                sh 'curl -u usuario:token -T target/*.jar https://tuservidor-artifactory/repositorio/'
            }
        }
    }
}
Agrega Jenkinsfile con pipeline completo
