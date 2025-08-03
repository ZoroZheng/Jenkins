pipeline {
    agent any
    
    stages {
        stage('Hello Jenkins') {
            steps {
                echo '🎉 Hello from Jenkins Pipeline!'
                echo "构建编号: ${env.BUILD_NUMBER}"
                echo "任务名称: ${env.JOB_NAME}"
            }
        }
        
        stage('Environment Check') {
            steps {
                echo '检查环境信息...'
                sh '''
                    echo "系统信息:"
                    uname -a
                    echo "当前时间: $(date)"
                    echo "工作目录: $(pwd)"
                    echo "目录内容:"
                    ls -la
                '''
            }
        }
        
        stage('Simple Test') {
            steps {
                echo '运行简单测试...'
                sh 'echo "✅ 测试 1: 通过"'
                sh 'echo "✅ 测试 2: 通过"'
                sh 'echo "✅ 测试 3: 通过"'
                echo '所有测试完成！'
            }
        }
        
        stage('Create Artifact') {
            steps {
                echo '创建构建产物...'
                sh '''
                    echo "Jenkins 构建信息" > build-result.txt
                    echo "构建时间: $(date)" >> build-result.txt
                    echo "构建编号: ${BUILD_NUMBER}" >> build-result.txt
                    echo "状态: 成功" >> build-result.txt
                '''
                
                // 归档文件
                archiveArtifacts artifacts: 'build-result.txt', fingerprint: true
                echo '✅ 构建产物已保存'
            }
        }
    }
    
    post {
        always {
            echo '🏁 Pipeline 执行完成'
        }
        success {
            echo '🎉 构建成功！'
        }
        failure {
            echo '❌ 构建失败，请检查日志'
        }
    }
}