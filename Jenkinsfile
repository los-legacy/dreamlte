node('ben') {
    timestamps {
        withEnv([
            'DEVICE=dreamlte',
            'BRANCH=lineage-17.1',
            'VERSION=17.1',
            'ROMTYPE=UNOFFICIAL',
            'OTA_ROMTYPE=unofficial',
            'SYSTEM_PATH=/home/benlue/android/lineage',
            'OUTPUT_PATH=/home/benlue/android/lineage/out/target/product',
            'OUT=/home/benlue/android/lineage/out',
            'URL=https://los-legacy.de',
            'SSH_URL=los-legacy.de',
            'LOCAL_MANIFESTS_URL=https://raw.githubusercontent.com/los-legacy/local_manifests/lineage-17.1/dream.xml',
            'LOCAL_MANIFESTS_PATH=.repo/local_manifests', 
            ]) {
            stage('Preparation') { // for display purposes
            
                checkout([$class: 'GitSCM', 
                branches: [[name: "$BRANCH"]], 
                doGenerateSubmoduleConfigurations: false, 
                extensions: [[$class: 'CleanBeforeCheckout', 
                deleteUntrackedNestedRepositories: true], 
                [$class: 'RelativeTargetDirectory', relativeTargetDir: '/home/benlue/android/lineage/build_script']], 
                submoduleCfg: [], 
                userRemoteConfigs: [[credentialsId: 'e1791597-2cce-40b2-8357-fcbc77a559d5', 
                url: "https://github.com/los-legacy/${DEVICE}.git"]]
                ])
                sh label: 'Preparation', script: 'source $SYSTEM_PATH/build_script/preparation.sh'
            }
            stage('RepoSync') { // for display purposes
                //sh label: 'RepoSync', script: 'source $SYSTEM_PATH/build_script/reposync.sh'
            }
            stage('Build') { // for display purposes
                sh label: 'Build', script: 'source $SYSTEM_PATH/build_script/build.sh'
            }
            stage('OTA Upload') { // for display purposes
                archiveArtifacts artifacts: '"$OUTPUT_PATH"/**/*.zip', fingerprint: true
                //sh label: 'OTA Upload', script: 'source $SYSTEM_PATH/build_script/upload.sh'             
            }
        }
    }
}
