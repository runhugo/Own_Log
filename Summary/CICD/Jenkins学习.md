# Jenkins学习记录

## Jenkinsfile
### 基本概念
1. Jenkinsfile是使用类似Groovy的语法编写
2. Jenkinsfile分为**声明式**和**脚本式**
3. 一个实现了基本的三阶段持续交付(CD)流水线（声明式）的Jenkinsfile如下：
```
Jenkinsfile (Declarative Pipeline)
pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}

合法的声明式流水线需要包括：
1. agent：指示Jenkins为流水线分配**执行器和工作区**
2. stages和stage：指示流水线都有包含什么阶段
3. steps：指示每个阶段中需要执行什么操作
```

###  阶段-构建
1. Jenkinsfile的作用：
    - 不是用来替代现有的构建工具（如GNU/Make，Maven，Gradle）
    - 它应该是将一个项目的开发周期中的多个阶段（如构建、测试、部署等）绑定在一起的粘合剂
2. 本阶段通常包括对源代码的组装、编译和打包
3. 构建成功后应该有相应的产物（比如Java构建后的jar包）
3. 示例：
```
Jenkinsfile (Declarative Pipeline)
pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'make' 
                archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true 
            }
        }
    }
}

1. **archiveArtifacts**：捕获与条件匹配的交付件（制品）
```

### 阶段-测试
1. 运行自动化测试是任何成功的持续交付过程的重要组成部分
2. 示例（JUnit）：
```
Jenkinsfile (Declarative Pipeline)
pipeline {
    agent any

    stages {
        stage('Test') {
            steps {
                /* `make check` 在测试失败后返回非零的退出码；
                * 使用 `true` 允许流水线继续进行
                */
                sh 'make check || true' 
                junit '**/target/*.xml' 
            }
        }
    }
}


1. **junit**: 捕获并关联与包含模式（\**/target/*.xml）匹配的 JUnit XML 文件
```

### 阶段-部属
1. 部属的步骤由项目或组织所决定
2. 一般来说，部属需要**构建**和**测试**阶段都通过了才会进行
3. 示例：
```
Jenkinsfile (Declarative Pipeline)
pipeline {
    agent any

    stages {
        stage('Deploy') {
            when {
              expression {
                currentBuild.result == null || currentBuild.result == 'SUCCESS' 
              }
            }
            steps {
                sh 'make publish'
            }
        }
    }
}
```