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

    stage('Docker Build Image') {
        imageBuild(CONTAINER_NAME, CONTAINER_TAG)
    }
}

def imageBuild(containerName, tag) {
    sh "docker build -t $containerName:$tag -t $containerName --pull --no-cache ."
    echo "Build da imagem Docker finalizado com sucesso!"
    sh "docker images"
}