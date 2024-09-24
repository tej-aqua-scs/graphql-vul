pipeline {
  agent any
  stages {
    stage('Aqua scanner') {
      agent {
        docker {
          image 'aquasec/aqua-scanner'
        }
      }
      steps {
        withCredentials([
          string(credentialsId: 'AQUA_KEY', variable: 'AQUA_KEY'),
          string(credentialsId: 'AQUA_SECRET', variable: 'AQUA_SECRET'),
          string(credentialsId: 'GITHUB_TOKEN', variable: 'GITHUB_TOKEN')
        ]){
          sh '''
            export TRIVY_RUN_AS_PLUGIN=aqua
            export AQUA_URL=https://api.supply-chain.cloud.aquasec.com
            export CSPM_URL=https://api.cloudsploit.com
            trivy --skip-db-update --cache-dir /tmp/trivy1251344953 fs --scanners misconfig,vuln,secret .
          '''
        }
      }
    }
  }
}
