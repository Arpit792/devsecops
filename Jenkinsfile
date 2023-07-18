pipeline {
  agent any
  stages {
    stage('Scan Secrets') {
      steps {
        sh '''#!/bin/bash

trufflehog --only-verified github --repo https://github.com/Arpit792/devsecops.git --fail

if [[ $? != 0 ]]
then
    echo "credentials found in the repo!!!"
fi'''
      }
    }

  }
}