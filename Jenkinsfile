#!/bin/env groovy

node {
    deleteDir()
    checkout scm
    files = sh(returnStdout: true, script: 'ls')
    println "list of property files"
    println files.split("\n").collect()[2,3]
    sh 'ls -la'
    
    fileprop = sh (returnStdout: true, script: 'ls | grep prop > fileproperty')

    liste1 = readFile 'fileproperty'
    
    File file1 = new File('${liste1}')
    def String yourData = file1.readLines()
    


    
    properties([
        parameters([
            choice(name: 'Param 1', choices: "${liste1}", description: 'Select param 1'),
            choice(name: 'Param 2', choices: "${yourData}", description: 'Select param 2')])])
    
}
