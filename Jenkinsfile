pipeline:
  agent: any
  stages:
    - name: Checkout
      steps:
        - script:
            name: Checkout the code from GitHub repository
            code: |
              checkout([$class: 'GitSCM',
                        branches: [[name: '*/master']],
                        doGenerateSubmoduleConfigurations: false,
                        extensions: [],
                        submoduleCfg: [],
                        userRemoteConfigs: [[url: 'https://github.com/automationbytes/CucumberPOMSep0223.git']]])

    - name: Build
      steps:
        - script:
            name: Run Maven to build the project using Windows batch command
            code: |
              bat "mvn -Dmaven.test.failure.ignore=true clean package"

    - name: Generate Cucumber HTML Reports
      steps:
        - script:
            name: Generate Cucumber HTML Reports
            code: |
              cucumber 'reports/json-reports/reports.json'

  post:
    always:
      - archiveArtifacts:
          artifacts: 'test-output/Html/ExtentHtml.html'
