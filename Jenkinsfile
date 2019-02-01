import groovy.json.JsonOutput
import groovy.json.JsonSlurperClassic 

// GLOBAL VARIABLE
def containers = '''
            {
                "containers" : [{
                    "name":"fx-proxy",
                    "tag":"a.azure.io/fx-proxy",
                    "dockerfile":"Dockerfile-proxy"
                }, {
                    "name":"fx-ep", 
                    "tag":"a.azure.io/fx-ep",
                    "dockerfile":"Dockerfile-ep"
                }]
            }
       '''

node {
   stage('Build') {
        // PARSE JSON
        def jsonSlurperClassic = new JsonSlurperClassic()
        def resultJson = jsonSlurperClassic.parseText(containers)
        for (i = 0; i < resultJson.containers.size(); i++){
          
          def tag = resultJson.containers[i].tag
          def name = resultJson.containers[i].name
          def dockerfile = resultJson.containers[i].dockerfile

          bat """
          @echo off
          REM for /f %%i in ('git config --get remote.origin.url') do set GIT_REPO=%%i
          REM for /f %%i in ('git rev-parse --abbrev-ref HEAD') do set GIT_BRANCH=%%i
          REM for /f "tokens=*" %%i in ('git log -1 --pretty^=format:"%%h - %%cd - %%cn" --date=format:"%%Y/%%m/%%d %%H:%%M:%%S"') do set GIT_COMMIT=%%i
          @echo on
          echo %GIT_REPO%
          echo %GIT_BRANCH%
          echo %GIT_COMMIT%
          echo ${tag}
          echo ${name}
          echo ${dockerfile}          
          """
        }
   }
}