# print all params
```
        stage('Initialization') {
            steps {
                script {
                    params.each {param ->
                      println "${param.key} -> ${param.value} "
                    }
                    ....
                }
            }
        }
```

# print all env
```
        stage('Initialization') {
            steps {
                script {
                    sh 'env | sort'
                    sh 'printenv | sort'
                    ....
                }
            }
        }
```