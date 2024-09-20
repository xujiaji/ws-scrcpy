pipeline {
    agent any

    stages {
        stage('Docker构建') {
            steps {
                trySh "docker rm -f ws-scrcpy"
                trySh "docker image rm xujiaji/ws-scrcpy"
                trySh "docker build -t xujiaji/ws-scrcpy ."
            }
        }
        stage('部署') {
            steps {
                trySh "docker run --name 'ws-scrcpy' -d  --net='host' -e TZ=\"Asia/Shanghai\" -e HOST_OS=\"Unraid\" -e HOST_HOSTNAME=\"Babay\" -e HOST_CONTAINERNAME=\"ws-scrcpy\" -e 'PUID'='99' -e 'PGID'='100' -l net.unraid.docker.managed=dockerman -l net.unraid.docker.webui='http://[IP]:[PORT:8000]/' -p '8000:8000/tcp' xujiaji/ws-scrcpy"
            }
        }
    }
}

def trySh(shtext) {
    try {
        sh shtext
    } catch(e) {
       throw e
    }
}
