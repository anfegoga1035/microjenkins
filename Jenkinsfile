pipeline {
    agent any

    stages {
        stage('Clonar el Repositorio'){
            steps {
                git branch: 'main', url: 'https://github.com/anfegoga1035/microjenkins.git'
            }
        }
        stage('Construir imagen de Docker'){
            steps {
                script {
                    withCredentials([
                        string(credentialsId: 'MONGO_URI', variable: 'MONGO_URI')
                    ]) {
                        docker.build('proyectos-micro:v1', '--build-arg MONGO_URI=${MONGO_URI} .')
                    }
                }
            }
        }
        stage('Desplegar contenedores Docker'){
            steps {
                script {
                    withCredentials([
                            string(credentialsId: 'MONGO_URI', variable: 'MONGO_URI')
                    ]) {
                        sh 'docker-compose up -d'
                    }
                }
            }
        }
    }

    post {
        always {
            emailext (
                subject: "Status del build: ${currentBuild.currentResult}",
                body: "Se ha completado el build. Puede detallar en: ${env.BUILD_URL}",
<<<<<<< HEAD
                to: "anfegoga1035@gmail.com",
                from: "andres.gomez@est.iudigital.edu.co"
=======
                to: "andres.gomez@est.iudigital.edu.co",
                from: "anfegoga1035@gmail.com"
>>>>>>> 22523720a019c49bdadc82cf8535d8b08f91ca2b
            )
        }
    }
}
