pipeline{
        agent any
        environment {
                DB_PASSWORD = "password"
        stages{
            stage('Clone repository'){
                steps{
                    sh "git clone https://gitlab.com/qacdevops/chaperootodo_client.git || true"
                }
            }
            stage('Install Docker'){
                steps{
                    sh "curl https://get.docker.com -S | sudo bash"
                    sh "sudo usermod -aG docker jenkins"
                }
            }
            stage('Install Docker Compose'){
                steps{
                    sh "sudo apt update"
                    sh "sudo apt install -y curl jq"
                    sh "version=\$(curl -s https://api.github.com/repos/docker/compose/releases/latest | jq -r '.tag_name')"
                    sh "sudo curl -L 'https://github.com/docker/compose/releases/download/1.27.4/docker-compose-\$(uname -s)-\$(uname -m)' -o /usr/local/bin/docker-compose"
                    sh "sudo chmod +x /usr/local/bin/docker-compose"
                 }
            }
            stage('Deploy'){
                 steps{
                    sh "cd chaperootodo_client && sudo docker-compose pull && docker-compose up -d"
                 }
            }
        }
}
