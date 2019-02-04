import groovy.json.JsonOutput
import groovy.json.JsonSlurperClassic 

@NonCPS
def jobExecute(def command){
    def sout = new StringBuilder(), serr = new StringBuilder()
    //def cmd = "docker build --no-cache --tag ${tag} --build-arg GIT_COMMIT_ID="%GIT_COMMIT% - %GIT_REPO% - %GIT_BRANCH%" --build-arg JENKINS_ID="%JOB_NAME% - %NODE_NAME% - %JENKINS_URL%" -f ${dockerfile} ."
    //def proc = 'docker ps'.execute()
    //def proc = "cmd /c echo ${name}".execute()
    def proc = command.execute()
    proc.consumeProcessOutput(sout, serr)
    proc.waitForOrKill(1000)
    //println "out>"
    //println "$sout"
    return "$sout"
}


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
          echo resultJson.containers[i].tag
          echo resultJson.containers[i].name
          echo resultJson.containers[i].dockerfile
          
          // def tag = resultJson.containers[i].tag
          // def name = resultJson.containers[i].name
          // def dockerfile = resultJson.containers[i].dockerfile
          
          // echo "${tag}"
          // echo "${name}"
          // echo "${dockerfile}"
          
          
          // bat """
          // @echo off
          // echo ${tag}
          // """
          
          /*
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
          */
        }
        
        // println "======================"
        
        // // set GIT_REPO
        // // GIT_REPO = jobExecute("git config --get remote.origin.url")
        // // set GIT_BRANCH
        // // GIT_BRANCH = jobExecute("git rev-parse --abbrev-ref HEAD")
        // //set GIT_COMMIT = jobExecute('git log -1 --pretty=format:"%h - %cd - %cn" --date=format:"%Y/%m/%d %H:%M:%S"')
        
        // // println "GIT_REPO: ${GIT_REPO}"
        // // println "GIT_BRANCH: ${GIT_BRANCH}"
        // //println "GIT_COMMIT: ${GIT_COMMIT}"
        
        // set blabla = jobExecute("cmd /c echo %PATH%")
        // println "${blabla}"
   }
}