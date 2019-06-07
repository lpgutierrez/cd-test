@Library('libpipelines@master') _

hose {
    EMAIL = 'cd'
    BUILDTOOLVERSION = '3.5.0'
    NEW_VERSIONING = 'true'
    AGENT = 'ubuntu-base-ssh-1604'
    ANCHORE_TEST = true
    DEPLOYONPRS = true
    GENERATE_QA_ISSUE = true

    ITSERVICES = [
        ['ZOOKEEPER': [
            'image': 'jplock/zookeeper:3.5.2-alpha',
            'env': [
                  'zk_id=1'],
            'sleep': 5]]]
    
    DEV = { config ->
        echo 'THIS IS MASTER'
        doCompile(config)
        doUT(config)
        doIT(config)
        doPackage(config)
	parallel(DEPLOY: {doDeploy(conf: config)},
		DOCKER: {doDocker(conf: config)},
		failFast: config.FAILFAST)
    }     
}
