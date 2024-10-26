#!groovy

@Library('roboshop-shared-library') _

// Our responsibility is to pass what type of application and component to pipeline to decide

def configMap = [
    application = 'nodejsVM'
    component = 'catalogue'
]

if( env.BRANCH_NAME.equalsIgnoreCase(main)){
    pipelineDecision.decidePipeline(configMap)
}
else{
    echo "This is production, deal with CR process"
}