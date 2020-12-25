pipeline {
    agent any
    stages {
        stage('Git pull') {
            steps {
                // 下载代码
                git 'https://github.com/rainCychen/building-a-multibranch-pipeline-project.git'
            }
        }
        stage('Build') {
            steps {
                // configId 即为之前配置的npm配置文件
                nodejs('node-v15.5.0') {
                    // npm 编译安装
                    sh 'npm install && npm run build'
                }
            }
        }
        stage('deploy') {
            steps {
                sshPublisher(publishers: [sshPublisherDesc(configName: "${server_name}", transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '/usr/local/nginx/html/jenkinsTest', remoteDirectorySDF: false, removePrefix: 'dist', sourceFiles: 'dist/**')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
            }
                
        }
    }
    
}