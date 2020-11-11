#!/usr/bin/env groovy

properties([
      pipelineTriggers([
            githubPush()
      ]),
      disableConcurrentBuilds()
])

def params = [
      repository  : 'https://github.com/BancoPopular/devops-infra-jenkins-jobs.git',
      credentials : 'leeroy-jenkins' 
]

rtServer (
    id: 'Artifactory-1',
    url: 'http://my-artifactory-domain/artifactory',
    // If you're using username and password:
    username: 'andres ',
    password: '1018454119.At',
    // If you're using Credentials ID:
    //credentialsId: 'ccrreeddeennttiiaall',
    // If Jenkins is configured to use an http proxy, you can bypass the proxy when using this Artifactory server:
    bypassProxy: true,
    // Configure the connection timeout (in seconds).
    // The default value (if not configured) is 300 seconds:
    timeout: 300
)