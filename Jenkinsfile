pipeline {
  agent any
  stages {
    stage('Scan Secrets') {
      steps {
        sh '''#!/bin/bash

wget https://github.com/trufflesecurity/trufflehog/releases/download/v3.44.0/trufflehog_3.44.0_linux_amd64.tar.gz
tar -xvf trufflehog_3.44.0_linux_amd64.tar.gz
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

  }
}