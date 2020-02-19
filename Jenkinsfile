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
    


    
    properties([
        parameters([
            choice(name: 'Param 1', choices: "${liste1}", description: 'Select param 1'),
            [$class: 'CascadeChoiceParameter', 
             choiceType: 'PT_SINGLE_SELECT',
             description: 'Property from file', 
             filterLength: 1,
             filterable: true, 
             name: 'Value', 
             randomName: 'choice-parameter-5631314456178619',
             referencedParameters: 'files',
             script: [
                 $class: 'GroovyScript',
                 script: [
                     classpath: [], 
                     sandbox: false, 
                     script: sh(returnStdout:true, script: 'cat ${liste2}')
                            ]]]])
    
}
