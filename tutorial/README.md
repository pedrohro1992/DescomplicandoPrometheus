# DescomplicandoPrometheus
Como instalar o Prometheus como Daemon no Linux

Baixar o prometheus com CURL:
 - curl -LO https://github.com/prometheus/prometheus/releases/download/v2.41.0/prometheus-2.41.0.linux-amd64.tar.gz 

Descompactar o arquivo .tar e entrar no diretório do prometheus:
 - tar -xvzf prometheus-2.41.0.linux-amd64.tar.gz && cd prometheus-2.41.0.linux-amd64
 
Mover os binários do prometheus e do proomtol para o /usr/local/bin
 - sudo mv prometheus-2.41.0.linux-amd64/prometheus /usr/local/bin
 - sudo mv prometheus-2.41.0.linux-amd64/promtool /usr/local/bin

Criar os diretórios necessários para o funcionamento do prometheus
 - sudo mkdir /etc/prometheus
 - sudo mkdir /var/lib/prometheus

Copiar o arquivo de configuração do prometheus(disponiveis em ~conf~) para o diretorio /etc/prometheus
 - sudo cp ./conf/prometheus.yml /etc/prometheus

Copiar os arquivos de consoles e de console_libraries para /etc/prometheus:
 - sudo mv prometheus-2.41.0.linux-amd64/consoles /etc/prometheus
 - sudo mv prometheus-2.41.0.linux-amd64/console_libraries /etc/prometheus

Criar o grupo e o usuário que o prometheus vai utilizar
 - sudo addgroup --system prometheus
 - sudo adduser --shell /sbin/nologin --system --group prometheus

Trocar o owner dos diretórios do prometheus:
 - sudo chown -R prometheus:prometheus /etc/prometheus
 - sudo chown -R prometheus:prometheus /var/lib/prometheus
 - sudo chown -R prometheus:prometheus /usr/local/bin/prometheus
 - sudo chown -R prometheus:prometheus /usr/local/bin/promtool

Copiar o arquivo de configuração do daemon para o diretório do systemd
 - sudo cp ./conf/prometheus.service /etc/systemd/system/prometheus.serive

Realizar o Reexec do daemon para atualizar o systemd:
 - sudo systemctl daemon-reexec

De o start do serviço do prometheus:
 - sudo systemctl start prometheus.service

Habilite o prometheus para começar no start da máquina:
 - sudo systemctl enable prometheus

