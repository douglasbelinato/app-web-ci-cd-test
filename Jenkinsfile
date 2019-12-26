def CONTAINER_NAME="app-test"
def CONTAINER_TAG="latest"

node {
    stage('Inicializa') {
        def dockerHome = tool 'myDocker'
        def mavenHome = tool 'myMaven'
        env.PATH = "${env.PATH}:${dockerHome}/bin:${mavenHome}/bin"
    }

    stage('Checkout') {
        checkout scm
    }

    stage('Maven Build') {
        sh "mvn clean package"
    }
}