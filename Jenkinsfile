pipeline {
  agent any
  stages {
    stage('Download and modify Update-Center Data') {
      steps {
        httpRequest(
                url: "https://updates.jenkins.io/update-center.json?id=default&amp;version=" + Jenkins.instance.version,
                consoleLogResponseBody: false,
                acceptType: 'APPLICATION_JSON',
                httpProxy: 'http://my.corporate.proxy:8080',
                outputFile: 'update-center.json'
        )
        script {
          updateCenterJson = readFile file: 'update-center.json'
          updateCenterJson = updateCenterJson.replaceAll("http:\\/\\/updates\\.jenkins-ci\\.org\\/download\\/", "http://archives.jenkins-ci.org/")
        }
        writeFile text: updateCenterJson, file: 'update-center-updated.json'
        archiveArtifacts 'update-center-updated.json'
      }
    }
  } 
}
