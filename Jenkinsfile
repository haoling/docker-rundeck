node('docker') {
    def VERSION="latest"
    stage('Preparation') { // for display purposes
        checkout scm
        if (! env.VERSION) VERSION="latest"
    }
    stage('Build') {
        def NO_CACHE_PARAM=""
        if (env.NO_CACHE.toBoolean()) NO_CACHE_PARAM="--no-cache"
        sh """#!/bin/bash
            sed -e 's#jordan/rundeck:latest#jordan/rundeck:2.10.8#' Dockerfile | docker build -t haoling/rundeck:${VERSION} ${NO_CACHE_PARAM} -
        """
    }
    stage('Push image') {
        sh "docker push haoling/rundeck:${VERSION}"
    }
}
