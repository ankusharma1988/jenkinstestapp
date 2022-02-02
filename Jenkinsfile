pipeline {
  agent any
  options {
        timeout(time: 4, unit: 'HOURS') 
    }   
  environment {
    APPSYSID = '1048541f1b410110089dc9961a4bcb48'
    CREDENTIALS = 'servicenow'
    DEVENV = 'https://hcltechdemosls4.service-now.com'
    TESTENV = 'https://hclnowintelligence.service-now.com'
    TESTSUITEID = 'bf8c266d732333005ce769972bf6a777'
  }
    

stages {
    stage('Build') {
      steps {
        snApplyChanges(appSysId: "${APPSYSID}", url: "${DEVENV}", credentialsId: "${CREDENTIALS}")
        snPublishApp(credentialsId: "${CREDENTIALS}", url: "${DEVENV}", appSysId: "${APPSYSID}",
          isAppCustomization: true, obtainVersionAutomatically: true, incrementBy: 2)
        snRunTestSuite(credentialsId: "${CREDENTIALS}", url: "${DEVENV}", testSuiteSysId: "${TESTSUITEID}", withResults: true)

        
       
        
      }
    }
    
    
    stage('Install'){
           steps {
        snDevOpsChange(
          snDevOpsStep()
        )
       snInstallApp(credentialsId: "${CREDENTIALS}", url: "${TESTENV}", appSysId: "${APPSYSID}", baseAppAutoUpgrade: false)
        
        
      }
    }


}

}
