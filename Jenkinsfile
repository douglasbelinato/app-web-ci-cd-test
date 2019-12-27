def CONTAINER_NAME="app-test"
def CONTAINER_TAG="latest"
def DOCKER_HUB_USER="dbelinato"

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

    stage('Docker Push Image') {
        withCredentials([usernamePassword(credentialsId: 'dockerHubAccount', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
            imagePush(CONTAINER_NAME, CONTAINER_TAG, USERNAME, PASSWORD)
        }
    }
}

def imageBuild(containerName, tag) {
    sh "docker build -t $containerName:$tag -t $containerName --pull --no-cache ."
    echo "Build da imagem Docker finalizado com sucesso!"
    sh "docker images"
}

def imagePush(containerName, tag, dockerUser, dockerPassword) {
    sh "docker login -u $dockerUser -p $dockerPassword"
    sh "docker tag $containerName:$tag $dockerUser/$containerName:$tag"
    sh "docker push $dockerUser/$containerName:$tag"
    echo "Push da imagem finalizado com sucesso!"
}