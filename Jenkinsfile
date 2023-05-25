properties([parameters([choice(choices: ['main', 'dila'], description: 'Git Branch List', name: 'Branch')])])

pipeline {
    agent any

    stages {
        stage('1st Ticket') {
            steps {
                echo 'EK-NDC-UAT Pipeline'
            }
        }
        
     stage('Checkout') {
     steps {
         // Checkout the Git repository
            git branch: "*/main", 
            credentialsId: 'github', 
            url: 'https://github.com/Pradeepde97/pipeline'
          }
        }
        stage('checkout') {
            steps {
               git url: 'https://github.com/Pradeepde97/pipeline',credentialsId: 'github', branch: "${params.Branch}"
        }
    }
       stage('deployment'){
        steps {
        sshagent(['newjenkin']) {
          sh  """
            ssh -o StrictHostKeyChecking=no test@192.168.8.111 << EOF
            sudo -i
            cd /home/test/pipeline
			docker system prune -a -f
            git pull origin ${params.Branch}
			make ENV=UAT rebuild
			exit
			exit
			exit
            EOF"""
        }
     }
    }
  }
}

