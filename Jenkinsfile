pipeline {
  agent any
  stages {
    stage('Scan Secrets') {
      steps {
        sh '''#!/bin/bash

wget -q https://github.com/trufflesecurity/trufflehog/releases/download/v3.44.0/trufflehog_3.44.0_linux_amd64.tar.gz
tar -xf trufflehog_3.44.0_linux_amd64.tar.gz
rm trufflehog_3.44.0_linux_amd64.tar.gz LICENSE README.md
mv trufflehog /tmp/trufflehog'''
        sh '''#!/bin/bash

/tmp/trufflehog --only-verified git https://github.com/Arpit792/devsecops --fail
if [[ $? != 0 ]]
then
    echo "credentials found in the repo!!!"
    exit 1
fi'''
      }
    }

    stage('sonarqube scan') {
      steps {
        sh '''#!/bin/bash

echo "downloading sonar-scanner ..."
wget -q https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-4.8.0.2856-linux.zip
unzip -qq sonar-scanner-cli-4.8.0.2856-linux.zip
rm -rf /tmp/sonar-scanner sonar-scanner-cli-4.8.0.2856-linux.zip
mv sonar-scanner-4.8.0.2856-linux /tmp/sonar-scanner

'''
        sh '''#!/bin/bash

/opt/maven/bin/mvn clean verify sonar:sonar \\
  -Dsonar.projectKey=devsecops \\
  -Dsonar.host.url=http://13.234.156.250:9000 \\
  -Dsonar.token=sqp_60d3cd0dfc8474ca2946f2d6cf03af6404e99fca
'''
      }
    }

  }
}