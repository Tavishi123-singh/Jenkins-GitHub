pipeline{
  agent any
  options {
  ansiColor('xterm')
  }
  parameters {
  choice choices: ['plan', 'apply'], description: 'Run terraform plan / apply', name: 'ACTION'
  gitParameter branchFilter: 'origin/(.*)', defaultValue: '', name: 'BRANCH', type: 'PT_BRANCH'
}
  stages {
  stage('Terraform plan') {
    steps {
      // One or more steps need to be included within the steps block.
      cleanWs()
      git branch: "${params.BRANCH}", url: ''
      dir
    }

    when {
      environment name: 'ACTION', value: 'plan'
    }
  }

  stage('Terraform apply') {
    steps {
      // One or more steps need to be included within the steps block.
    }

    when {
      environment name: 'ACTION', value: 'apply'
    }
  }

  }
}
