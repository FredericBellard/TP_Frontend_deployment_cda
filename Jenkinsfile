pipeline {
    agent {
        label 'agent-node'
        
    }
    stages {
        stage('Installer dépendances') {
            steps {
                git branch: 'main', url: 'https://github.com/FredericBellard/TP_Frontend_deployment_cda.git'
            }
        }
        stage('Déploiement') {
            steps {
                   sh """
                    lftp -d -u ${Login},${Mdp} ${Lienftp} -e "
                        mirror -R /home/jenkins/workspace/fred_TP_Frontend_deployment_cda/ www/;
                        bye
                    "
                """             
            }
        }
        stage('npm'){
            steps{
                sh """
                    sshpass -p ${Mdp} ssh -o StrictHostKeyChecking=no ${Lienssh} '
                    cd www/ &&
                    npm install
                    '
                """    
            }
        }

    }
}
