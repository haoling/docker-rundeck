node('docker') {
    def app
    def VERSION="latest"
    stage('Preparation') { // for display purposes
        checkout scm
        if (! env.VERSION) VERSION=env.VERSION
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
        docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
            app.push(VERSION);
        }
    }
}
