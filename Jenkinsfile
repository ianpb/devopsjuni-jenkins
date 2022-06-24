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
    stage("Deploy") {
       docker.image('ubuntu').inside('-u root') {
          sh 'echo "Ini adalah Deploy"'
       }
    }
}