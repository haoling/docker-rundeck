node('docker') {
    def app
    def VERSION
    stage('Preparation') { // for display purposes
        checkout scm
        if (! VERSION) VERSION="latest"
    }
    stage('Build') {
        def PARAM="."
        if (env.NO_CACHE.toBoolean()) PARAM="--no-cache ${PARAM}"
        sh "sed -e 's#jordan/rundeck:latest#jordan/rundeck:${VERSION}#' Dockerfile"
        app = docker.build("haoling/rundeck", PARAM)
        cleanWs()
    }
    stage('Push image') {
        docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
            //app.push(VERSION);
        }
    }
}
