pipeline{
  //agent any
  agent {
  label 'tfslave'
  }
  options {
  ansiColor('xterm')
  }
  parameters {
  	choice choices: ['plan', 'apply'], description: 'Run terraform plan / apply', name: 'ACTION'
  	gitParameter branchFilter: 'origin/(.*)', defaultValue: '', name: 'BRANCH', type: 'PT_BRANCH'
  	string (name: 'PROFILE', defaultValue: 'myprofile', description: 'Optional. Target aws profile defaults to myprofile')
  }
	
  environment {
  	AWS_ACCESS_KEY_ID = credentials('AWS_ACCESS_KEY_ID')
  	AWS_SECRET_ACCESS_KEY = credentials('AWS_SECRET_ACCESS_KEY')
 }

  stages {
	  stage('checkout'){
		  steps{
			  script{
				  dir('./terraform'){
					git branch: "${params.BRANCH}", url: 'https://github.com/Tavishi123-singh/Jenkins-GitHub.git'
					//checkout scm
				  }
			  }
		}
	  }
  stage('Terraform plan') {
    when {
      expression { ACTION == 'plan'}
    }
    steps {
      // One or more steps need to be included within the steps block.
      //cleanWs()
      git branch: "${params.BRANCH}", url: 'https://github.com/Tavishi123-singh/Jenkins-GitHub.git'
      dir("./terraform"){
	      //cmd_exec('cd ./terraform')
	      //cmd_exec('echo "EXECUTING TERRAFORM PLAN !!"')
	      //cmd_exec('terraform init && terraform plan')
	//bat "cd ./terraform"
	bat 'echo "EXECUTING TERRAFORM PLAN !!"'
      	bat 'terraform init && terraform plan'
      }
    
  }
  }
  /*def cmd_exec(command) {
    return bat(returnStdout: true, script: "${command}").trim()
  }*/
  stage('Terraform apply') {
     when {
       expression { ACTION == 'apply'}
    }
    steps {
      // One or more steps need to be included within the steps block.
      git branch: "${params.BRANCH}", url: 'https://github.com/Tavishi123-singh/Jenkins-GitHub.git'
      dir("./terraform"){
      	bat 'echo "EXECUTING TERRAFORM APPLY !!"'
      	bat 'terraform init && terraform apply --auto-approve'
      }
   
  }
  }
  }
}
