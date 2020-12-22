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