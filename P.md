## Docker
- start all
    ```
        docker start $(docker ps -a | awk '{ print $1}' | tail -n +2)
    ```
    - ~~这里可能存在mac和linux的区别.$或许不应该加入~~ `发现原因.是因为fish shell 导致的 换用bash没有问题`
    - 该命令类似的可以使用到更多的docker通用命令上