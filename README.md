# Kubernetes: Guia essencial :rocket:

Este repositório foi criado para ajudar no estudo e a compreender os conceitos-chave do Kubernetes e como utilizá-lo para orquestrar contêineres de maneira eficiente. Aqui você encontrará uma introdução teórica, exemplos práticos e dicas úteis para explorar essa poderosa ferramenta.
<hr>

#### :book: O que é Kubernetes?
Kubernetes (K8s) é uma plataforma de código aberto para automação de implantação, escalonamento e gerenciamento de aplicações em contêineres. Ele foi originalmente desenvolvido pelo Google e é agora mantido pela Cloud Native Computing Foundation (CNCF).

Em outras palavras o Kubernetes é um orquestrador de container.
<!--
🧩 Conceitos-chave
-->
#### :key: Principais Conceitos

* **Container:** Container é uma tecnologia de virtualização usada para empacotar e isolar aplicações e suas dependências, ou seja, container é isolamento de recursos. 
    * **Container engine:** É o responsável por gerenciar as imagens e volumes, ele é o responsável por garantir que os os recursos utilizados pelos containers estão devidamente isolados, a vida do container, storage, rede, etc, ou seja, é o responsável por criar o container e verificar se ele esta funcionando corretamente, são exemplos de container engine: Docker Engine e o Podman.
    
    * **Container runtime:** é o responsável por executar os containers nos nós. Quando você está utilizando ferramentas como Docker ou Podman para executar containers em sua máquina, por exemplo, você está fazendo uso de algum Container Runtime, ou melhor, o seu Container Engine está fazendo uso de algum Container Runtime, em outras palavras ele é o responsável por fazer as comunicações entre o container engine e o Kernel do host. (Ele executa os containeres)

        Temos três tipos de Container Runtime:

        * **Low-level:** são os Container Runtime que são executados diretamente pelo Kernel, como o runc, o crun e o runsc.

        * **High-level:** são os Container Runtime que são executados por um Container Engine, como o containerd, o CRI-O e o Podman.

        * **Sandbox e Virtualized:** são os Container Runtime que são executados por um Container Engine e que são responsáveis por executar containers de forma segura. O tipo Sandbox é executado em unikernels ou utilizando algum proxy para fazer a comunicação com o Kernel. O gVisor é um exemplo de Container Runtime do tipo Sandbox. Já o tipo Virtualized é executado em máquinas virtuais. A performance aqui é um pouco menor do que quando executado nativamente. O Kata Containers é um exemplo de Container Runtime do tipo Virtualized.

* **OCI (Open Container Initiative):** A OCI é uma organização sem fins lucrativos que tem como objetivo padronizar a criação de containers, para que possam ser executados em qualquer ambiente. A OCI foi fundada em 2015 pela Docker, CoreOS, Google, IBM, Microsoft, Red Hat e VMware e hoje faz parte da Linux Foundation.

O runc, principal projeto desenvolvido pela OCI, é um container runtime de baixo nível amplamente utilizado por diversos Container Engines, incluindo o Docker. Este projeto, totalmente open source, é escrito em Go e seu código fonte pode ser acessado no GitHub.

* Workers:

* **Cluster:** É o ambiente do kubernetes e é composto por:
    * **Master (control plane):** responsável por gerenciar o cluster.
    * **Nodes:** Máquinas (físicas ou virtuais) que executam os containers.
* Pods
* Deployments
* Services
* Namespaces
* ConfigMap e secret

#### :: Instalação 

#### :folder: Estrutura do Repositório

#### Exemplos práticos

#### :chain: Recursos adicionais

#### Boas Práticas

#### Referências
* https://kubernetes.io
* https://github.com/kubernetes/kubernetes/
* https://github.com/kubernetes/kubernetes/issues
* https://github.com/badtuxx/DescomplicandoKubernetes?tab=readme-ov-file

Abaixo temos as páginas oficiais das certificações do Kubernetes (CKA, CKAD e CKS):

* https://www.cncf.io/certification/cka/
* https://www.cncf.io/certification/ckad/
* https://www.cncf.io/certification/cks/

#### Contribuições
![Rocket Icon](https://img.shields.io/badge/Launch-Rocket-blue?logo=rocket)
