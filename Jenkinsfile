pipeline {
    agent any

    stages {
        stage('sg_cli_jobs') {
            steps {
                script {
                    def dockerImage = 'ubuntu:latest'
                    def sgBaseUrl = env.SG_BASE_URL
                    def sgApiToken = env.SG_API_TOKEN
                    def sgDashboardUrl = env.SG_DASHBOARD_URL
                    def sgOrg = env.SG_ORG
                    def sgWorkflowGroup = env.SG_WORKFLOW_GROUP
                    
                    docker.image(dockerImage).inside {
                        sh 'apt-get update && apt-get install -y wget jq curl'
                        sh 'wget https://raw.githubusercontent.com/StackGuardian/sg-cli/main/shell/sg-cli -O sg-cli'
                        sh "bash sg-cli stack create --org ${sgOrg} --workflow-group ${sgWorkflowGroup} -- payload.json"
                    }
                }
            }
        }
    }

    environment {
        SG_BASE_URL = "$SG_BASE_URL"
        SG_API_TOKEN = "$SG_API_TOKEN"
        SG_DASHBOARD_URL = "$SG_DASHBOARD_URL"
        SG_ORG = "$SG_ORG"
        SG_WORKFLOW_GROUP = "$SG_WORKFLOW_GROUP"
    }
}