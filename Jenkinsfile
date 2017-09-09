/*  vim: set syntax=groovy:

  This is the Jenkinsfile which will build pipeline job "openstack-extensions-6wind"

  openstack-upgrade-scripts is a parameterized job, with the parameters listed below
    - NUAGE_PROJECT
    - NUAGE_BUILD_RELEASE
    - NUAGE_BUILD_NUMBER
    - DEPLOY_DIR
    - BUILD_DISPLAY_NAME
    - OPENSTACK_EXTENSIONS_6WIND_PATH
*/

currentBuild.displayName = "${BUILD_DISPLAY_NAME}"

def globalDir = getGlobalDir()
def sixWindLink = "6wind"
def deployDir

node('master') {
    stage('determine 6wind path') {
        deployDir = env.OSC_DEPLOY_DIR ?: "${globalDir}/${DEPLOY_DIR}"
    }

    stage('link 6wind builds') {
        if (env.OPENSTACK_EXTENSIONS_6WIND_PATH) {
            sh """
                ssh -o StrictHostKeyChecking=no \
                    testlab@strato.us.alcatel-lucent.com "test -d ${deployDir} || mkdir -p ${deployDir}"
            """

            sh """
                ssh -o StrictHostKeyChecking=no \
                    testlab@strato.us.alcatel-lucent.com "cd ${deployDir} && ln -sv ${OPENSTACK_EXTENSIONS_6WIND_PATH}  ${sixWindLink}"
            """
        } else {
            error "param OPENSTACK_EXTENSIONS_6WIND_PATH is not set"
        }
    }
}
