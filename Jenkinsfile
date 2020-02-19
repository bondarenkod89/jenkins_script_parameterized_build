#!/bin/env groovy

node {
    deleteDir()
    checkout scm
    files = sh(returnStdout: true, script: 'ls')
    println "list of property files"
    println files.split("\n").collect()[1,2]
    sh 'ls -la'
    
    fileprop = sh (returnStdout: true, script: 'ls | grep prop > fileproperty')

    liste1 = readFile 'fileproperty'
    liste2 = readFile '${liste1}'
    


    
    properties([parameters([choice(name: 'Param 1', choices: "${liste1}", description: 'Select param 1'),
                            choice(name: 'Param 2', choices: "${liste2}", description: 'Select param 2')])])
    
    sh 'echo Hello World'
    
}
