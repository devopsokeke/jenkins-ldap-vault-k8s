pipeline {
    agent any
    stages {
        stage('Revoke Token') {
            steps {
                script {
                    sh """
                    curl -s --header "X-Vault-Token: ${env.VAULT_TOKEN}" \
                         --request POST \
                         http://vault.example.com/v1/auth/token/revoke-self
                    """
                    echo "Vault token revoked."
                }
            }
        }
    }
}
pipeline {
    agent any
    stages {
        stage('Debug Trigger') {
            steps {
                script {
                    def cause = currentBuild.rawBuild.getCause(hudson.model.Cause$UserIdCause)
                    if (cause) {
                        echo "Triggered by user: ${cause.userId}"
                    } else {
                        echo "Build trigger information unavailable. Was this build triggered manually?"
                    }
                }
            }
        }
    }
}
