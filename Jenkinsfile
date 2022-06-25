node {
    checkout scm

    // build
    stage("Build"){
        docker.image('shippingdocker/php-composer:7.4').inside('-u root') {
            sh 'rm composer.lock'
            sh 'composer install'
        }
    }


    // Testing
    stage("Test") {
       docker.image('ubuntu').inside('-u root') {
          sh 'echo "Ini adalah Test"'
       }
    }   

    // Testing
    stage("Deploy"){
       docker.image('agung3wi/alpine-rsync:1.1').inside('-u root') {
          sshagent (credentials: ['ssh-dev']) {
             sh 'mkdir -p ~/.ssh'
             sh 'ssh-keyscan -H "$IP_DEV" > ~/.ssh/known_hosts'
             //rsync, to sync folder ./ at afb756cb1ae5 agung3wi/alpine-rsync yg mana dijalankan melalui /var/jenkins_home/workspace/deploy_dev 
             //di container aff635ac6207(myjenkins-blueocean),then pushed the content of the said directory to a remote directory 
             // at /home/ubuntu/dev.aijalon.xyz at dev.aijalon.xyz VM 
             sh "rsync -rav --delete ./ ubuntu@$IP_DEV:/home/ubuntu/dev.aijalon.xyz/ --exclude=.env --exclude=storage --exclude=.git"
            }
        }
    }    
}