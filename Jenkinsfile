pipeline {
    stages {
        stage('Git pull') {
            steps {
                // 下载代码
                git  branch: "${params.BRANCH}", url: 'git@github.com:rainCychen/building-a-multibranch-pipeline-project.git'
            }
        }
        stage('Build') {
            steps {
                // configId 即为之前配置的npm配置文件
                nodejs(nodeJSInstallationName: 'node-v15.5.0', configId: 'npm-config') {
                    // npm 编译安装
                    sh 'npm install && npm run build'
                }
            }
        }
        stage('deploy') {
        sshPublisher(publishers: [sshPublisherDesc(configName: "${server_name}", transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '/usr/local/nginx/html/jenkinsTest', remoteDirectorySDF: false, removePrefix: 'dist', sourceFiles: 'dist/**')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
        }
    }
    
}