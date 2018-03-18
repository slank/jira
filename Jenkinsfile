#!/usr/bin/env groovy

  node('master') {

      try {

          // we don't want any leftovers to influence our execution (like previous logs)
          step([$class: 'WsCleanup'])

          checkout scm

          stage("test") {
            sh "tox"
          }

      } // end-try
      catch (ex) {
          println "Exception ${ex.getClass()} received: ${ex}"
          error = ex
          currentBuild.result = 'FAILURE'
          throw ex
      }
      finally {
          stage('archive') {

              archiveArtifacts artifacts: '.envrc',
                               fingerprint: false,
                               allowEmptyArchive: true
              // defaultExcludes: true
              // caseSensitive: false
              // onlyIfSuccessful: false
          } // end-clean
      } // finally
  } // node
