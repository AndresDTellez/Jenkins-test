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

node {
      def error = null
      try {
            env.DSL_SCRIPTS_PATH = 'DSL-Scripts'
            checkout(params.repository, params.credentials, env.BRANCH_NAME)
            loadDSLJobs(env.DSL_SCRIPTS_PATH)
      }
      catch(caughtError){
            error = caughtError
            currentBuild.result = 'FAILURE'
      }
      finally{
            notifyBuild(currentBuild.result)
            cleanWs()
            if(error){
                  echo "Fallo al ejecutar JOB \u274C"
                  throw error
            }
      }
}


def checkout(repository, credentials, branch){
      checkout([
            $class: 'GitSCM',
            branches: [[name: branch]],
            doGenerateSubmoduleConfigurations: false,
            extensions: [],
            submoduleCfg: [],
            userRemoteConfigs: [[
            credentialsId: credentials,
            url: repository
            ]]
      ])
}

def loadDSLJobs(path){
      stage('Load DSL'){
            echo "Cargando archivos de configuracion \u2705"
            jobDsl targets: 'DSL-Scripts/*/.groovy', ignoreExisting: false
            echo "Se cargan Jobs correctamente \u2705"
      }
}

def notifyBuild(String buildStatus = 'STARTED'){
      stage('notifyBuild'){
            buildStatus = buildStatus ?: 'SUCCESS'
            echo "${buildStatus}"
      }
}