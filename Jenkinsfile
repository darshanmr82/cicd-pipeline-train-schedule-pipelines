pipeline 
{
  agent any
  stages 
  {
    stage ('Build Gradle project') 
    {
      steps 
      {
        echo 'Running build automation'
        sh './gradlew build --no-daemon'
        archiveArtifacts artifacts: 'dist/trainSchedule.zip'
      }
    }
    stage('Snyk - SCA Monitor on master') 
    {
        steps 
        {
          script 
          {
              echo 'Running Snyk SCA monitor - this will push the dependency list from master up to Snyk to produce and maintain an online report on all vulns (not just high)'
              snykSecurity(snykTokenId: 'POC-token-jenkins', snykInstallation: 'Snyk-Latest', failOnIssues: false, monitorProjectOnBuild: true, severity: 'low')
          }
        }
    }
  }
}
