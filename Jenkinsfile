node('docker') {
    def app
    def VERSION="latest"
    stage('Preparation') { // for display purposes
        checkout scm
        if (! env.VERSION) VERSION="latest"
    }
    stage('Build') {
        def PARAM="."
        if (env.NO_CACHE.toBoolean()) PARAM="--no-cache ${PARAM}"
        sh """#!/bin/bash
            sed -i -e 's#jordan/rundeck:latest#jordan/rundeck:${VERSION}#' Dockerfile
        """
        app = docker.build("haoling/rundeck", PARAM)
        cleanWs()
    }
    stage('Push image') {
        withDockerRegistry([credentialsId: 'docker-hub-credentials', url: 'https://hub.docker.com']) {
            app.push(VERSION);
        }
    }
}
