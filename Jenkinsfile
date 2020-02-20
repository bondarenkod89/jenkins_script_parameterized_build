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
    liste2 = readFile "${liste1}"
    sh 'ls -la'

//    for (def i=0;i<=2;i++){
//        log.info file1.readLines().get(i)
//    File file1 = new File()
//    def String yourData = file1.readLines()
//    }
   
    properties([
        parameters([
            choice(name: 'Param 1', choices: "${liste1}", description: 'Select param 1'),
            choice(name: 'Param 2', choices: "${yourData}", description: 'Select param 2')])])
    
}
