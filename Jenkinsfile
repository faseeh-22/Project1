

pipeline {
    agent any
    parameters {
        string(defaultValue: 'dashboard.ndjson', description: 'Enter the filename:', name: 'FILENAME')
        string(defaultValue: 'Product', description: 'Enter the replacement word for Product_name:', name: 'PRODUCT')
        string(defaultValue: 'Endpoint', description: 'Enter the replacement word for Endpoint_name:', name: 'ENDPOINT')
        string(defaultValue: 'Request_uri', description: 'Enter the replacement word for Request_uri:', name: 'REQ_URI')
        string(defaultValue: 'Index-pattern', description: 'Enter the replacement word for Index-pattern:', name: 'INDEX')
        string(defaultValue: 'rename_file', description: 'Enter the rename file', name: 'RENAME')
    }
    stages {
        stage('Fetch File from GitHub') {
            steps {
                script {
                    // Checkout code from your Git repository
                    checkout([$class: 'GitSCM', branches: [[name: '*/main']],
                              doGenerateSubmoduleConfigurations: false,
                              extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/faseeh-22/Project1.git']]])
                }
            }
        }
        stage('Execute Script') {
            steps {
                // Set execute permission on the script file (if needed)
                sh 'chmod +rwx final1.sh'
                // Execute your Bash script with parameters
                script {
                    sh "./final1.sh ${params.FILENAME} ${params.PRODUCT} ${params.ENDPOINT} ${params.REQ_URI} ${params.INDEX} ${params.RENAME}"
                }
            }
        }
        stage('Copy File to Local Repository') {
    steps {
        // Copy the updated file to a specific location in your local repository
        sh "sudo cp /var/lib/jenkins/workspace/OS/${params.FILENAME} /home/faseeh/OS-Project"
        sh "sudo mv /home/faseeh/OS-Project/${params.FILENAME} /home/faseeh/Downloads/${params.RENAME}"
    }
}
    }
}
