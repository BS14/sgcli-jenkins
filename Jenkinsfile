pipeline {
    agent any

    stages {
        stage('sg_cli_jobs') {

            environment {
               SG_BASE_URL = "https://api.app.stackguardian.io"
               SG_DASHBOARD_URL = "https://app.stackguardian.io/orchestrator"
               SG_ORG = "stackguardian"
               SG_WORKFLOW_GROUP = "jenkinsci"
            }

            steps {
                script {
                    def SG_API_TOKEN = credentials('SG_API_TOKEN')
                    
                    // Checkout the code
                    checkout scm

                    // Install necessary tools
                    sh 'apt-get update && apt-get install -y wget jq curl'

                    // Download sg-cli
                    sh 'wget https://raw.githubusercontent.com/StackGuardian/sg-cli/main/shell/sg-cli -O sg-cli'

                    // Run sg-cli command
                    sh "bash sg-cli stack create --org ${SG_ORG} --workflow-group ${SG_WORKFLOW_GROUP} -- payload.json"
                }
            }
        }
    }
}
