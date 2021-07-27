# ranchergui
Pequeno projeto para laboratorios rancher


## O que faz

Por enquanto sobe um master para a instalação do rancher e seus respectivos nodes.  
Não serão adicionados scripts de instalação e/ou provisionamento, uma vez que este projeto visa o exercicio e o aprendizado das praticas de implementação do Rancher.  

Caso esteja buscando algo mais completo, você pode verificar a [Documentação Oficial](https://rancher.com/docs/rancher/v2.x/en/quick-start-guide/deployment/quickstart-vagrant/)

## Requerimentos

Vagrant  
Virtualbox  

É necessária a disponibilização de recursos de sua maquina local:  


**Master** :
  - 4GB RAM
  - 2vCPUS  


**Nodes** :
  - 2GB RAM
  - 1vCPU
  
 Por default o *VagrantFile* está configurado para criar 1 master-node e 2 nodes. Essas configurações podem ser facilmente alteradas no mesmo arquivo.



## Como usar

```
vagrant up (para subir o ambiente)

vagrant destroy (para deletar o ambiente)

vagrant ssh <maquina> (para logar no host)
```

Algumas vezes o vagrant pode apresentar erros ao instalar as boxes, por isso é recomendado a execução dos comandos abaixo que vão instalar os plug-ins necessários para o funcionamento.

```
vagrant plugin install vagrant-vboxmanage

vagrant plugin install vagrant-vbguest
```

## Como instalar o Rancher

```
docker run -d --restart=unless-stopped \
-p 80:80 -p 443:443 \
-v /opt/rancher:/var/lib/rancher \
--privileged \
rancher/rancher:v2.5.4
```

