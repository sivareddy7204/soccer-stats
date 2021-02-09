#!groovy​

// FULL_BUILD -> true/false build parameter to define if we need to run the entire stack for lab purpose only
final FULL_BUILD = params.FULL_BUILD
// HOST_PROVISION -> server to run ansible based on provision/inventory.ini
final HOST_PROVISION = params.HOST_PROVISION

final GIT_URL = 'https://github.com/sivareddy7204/soccer-stats.git'
final NEXUS_URL = 'nexus.local:8081'


stage('Build') {
    node {
        git GIT_URL

            if(FULL_BUILD) {
                sh "mvn clean install "
                
            }
        }
    }


if(FULL_BUILD) {
    stage('Unit Tests') {   
        node {
            
                sh "mvn -B clean test"
                stash name: "unit_tests", includes: "target/surefire-reports/**"
            }
        }
    }


if(FULL_BUILD) {
    stage('Integration Tests') {
        node {
            
                sh "mvn -B clean verify -Dsurefire.skip=true"
                stash name: 'it_tests', includes: 'target/failsafe-reports/**'
            }
        }
    }


