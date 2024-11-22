# Kubernetes: Guia essencial :rocket:

Este repositório foi criado para ajudar no estudo e a compreender os conceitos-chave do Kubernetes e como utilizá-lo para orquestrar contêineres de maneira eficiente. Aqui você encontrará uma introdução teórica, exemplos práticos e dicas úteis para explorar essa poderosa ferramenta.
<hr>

#### :book: O que é Kubernetes?
Kubernetes (K8s) é uma plataforma de código aberto para automação de implantação, escalonamento e gerenciamento de aplicações em contêineres. Ele foi originalmente desenvolvido pelo Google e é agora mantido pela Cloud Native Computing Foundation (CNCF).

Em outras palavras o Kubernetes é um orquestrador de container.

#### :key: Principais Conceitos

* **Container:** Container é uma tecnologia de virtualização usada para empacotar e isolar aplicações e suas dependências, de forma simples, container é isolamento de recursos. 
    * **Container engine:** É o responsável por gerenciar as imagens e volumes, ele é o responsável por garantir que os os recursos utilizados pelos containers estão devidamente isolados, a vida do container, storage, rede, etc, ou seja, é o responsável por criar o container e verificar se ele esta funcionando corretamente, são exemplos de container engine: Docker Engine e o Podman.  
    
    * **Container runtime:** é o responsável por executar os containers nos nós. Quando você está utilizando ferramentas como Docker ou Podman para executar containers em sua máquina, por exemplo, você está fazendo uso de algum Container Runtime, ou melhor, o seu Container Engine está fazendo uso de algum Container Runtime, em outras palavras ele é o responsável por fazer as comunicações entre o container engine e o Kernel do host. (Ele executa os containeres).  
        Temos três tipos de Container Runtime:
        * **Low-level:** são os Container Runtime que são executados diretamente pelo Kernel, como o runc, o crun e o runsc.
        * **High-level:** são os Container Runtime que são executados por um Container Engine, como o containerd, o CRI-O e o Podman.
        * **Sandbox e Virtualized:** são os Container Runtime que são executados por um Container Engine e que são responsáveis por executar containers de forma segura. O tipo Sandbox é executado em unikernels ou utilizando algum proxy para fazer a comunicação com o Kernel. O gVisor é um exemplo de Container Runtime do tipo Sandbox. Já o tipo Virtualized é executado em máquinas virtuais. A performance aqui é um pouco menor do que quando executado nativamente. O Kata Containers é um exemplo de Container Runtime do tipo Virtualized.\

* **OCI (Open Container Initiative):** A OCI é uma organização sem fins lucrativos que tem como objetivo padronizar a criação de containers, para que possam ser executados em qualquer ambiente. A OCI foi fundada em 2015 pela Docker, CoreOS, Google, IBM, Microsoft, Red Hat e VMware e hoje faz parte da Linux Foundation.
O runc, principal projeto desenvolvido pela OCI, é um container runtime de baixo nível amplamente utilizado por diversos Container Engines, incluindo o Docker. Este projeto, totalmente open source, é escrito em Go e seu código fonte pode ser acessado no GitHub.

* **Cluster:** É o ambiente do kubernetes e é composto por:
    * **Master (control plane):** responsável por gerenciar o cluster possui a resposabilidade de armazenar o estado do cluster e de manter a saúde e disponibilidade do cluster.
    * **Nodes:** Máquinas (físicas ou virtuais) que executam os containers.

* **Pods:**

* **Deployments:**

* **Services:**

* **ReplicaSets:**

* Namespaces

* ConfigMap e secret

### 🧩 Arquitetura do K8S
Assim como os demais orquestradores disponíveis, o k8s também segue um modelo control plane/workers, constituindo assim um cluster, onde para seu funcionamento é recomendado no mínimo três nós: o nó control-plane, responsável (por padrão) pelo gerenciamento do cluster, e os demais como workers, responsáveis por executar as aplicações.

![k8s architecture](./img/kubernetes_archiketktur_blog.webp)

* **Control Plane:** Como já sabemos o ***Control Plane*** é o responsável por gerenciar o cluster, mantendo a saúde e disponibilidade do ambiente kubernetes.
**Componentes de um Control Plane**
    * **etcd:** É um datastore chave-valor distribuído que o kubernetes utiliza para armazenar as especificações, status e configurações do cluster, ele conversa com o Kube ApiServer.
    * **Kube ApiServer (API Server):** É o ponto de entrada para todas as interações com o cluster recebendo comandos e ou solicitações via kubectl, dashboards ou APIS externas. Ele server como intermediário entre os outros componentes do cluster. Todas as comunicações passam por ele. 
    * **Kube Scheduler:**  É o responsável por selecionar o nó que irá hospedar um determinado pod para ser executado. Esta seleção é feita baseando-se na quantidade de recursos disponíveis em cada nó, como também no estado de cada um dos nós do cluster, garantindo assim que os recursos sejam bem distribuídos.
    * **Kube Controller:** É o controller manager quem garante que o cluster esteja no último estado definido no etcd. Por exemplo: se no etcd um deploy está configurado para possuir dez réplicas de um pod, é o controller manager quem irá verificar se o estado atual do cluster corresponde a este estado e, em caso negativo, procurará conciliar ambos.

    ![Arquitetura do Control Plane](./img/Control_Plane_arq.png)\

* **Workers:** São os nodes onde as aplicações estão rodando, ele é o responsável por executar aplicações e suas cargas de trabalho.
    ***Principais funções de um Worker***
    1. **Execução de Pods:** Os Workers hospedam e executam os Pods, que são gerenciados pelo Control Plane.
    2. **comunicação com o Control plane:** Cada nó worker comunica-se com o nó mestre (ou Control Plane) para receber instruções sobre quais cargas de trabalho devem ser executadas.
    3. **Fornecimento de recursos:** Ele fornece CPU, memória, rede e armazenamento para os containeres rodarem.

    ***Componentes de um worker***
    Os nós workers possuem alguns componentes principais que permitem sua operação:
    1. **Kubelet:** O kubelet desempenha o papel de um agente do k8s que é executado nos nós workers. Em cada nó worker deverá existir um agente Kubelet em execução, encarregado de gerenciar efetivamente os pods direcionados pelo controller do cluster dentro dos nós. Para isso, o Kubelet pode iniciar, parar e manter os contêineres e os pods em funcionamento seguindo as instruções fornecidas pelo controlador do cluster;
    2. **Kube-proxy:** Age como um proxy e um load balancer. Este componente é responsável por efetuar roteamento de requisições para os pods corretos, como também por cuidar da parte de rede do nó.



### Instalação

É possível criar um cluster Kubernetes rodando em apenas um nó, porém é recomendado somente para fins de estudos e nunca executado em ambiente produtivo.

Caso você queira utilizar o Kubernetes em sua máquina local, em seu desktop, existem diversas soluções que irão criar um cluster Kubernetes, utilizando máquinas virtuais ou o Docker, por exemplo.

Com isso você poderá ter um cluster Kubernetes com diversos nós, porém todos eles rodando em sua máquina local, em seu desktop.

Alguns exemplos são:

Kind: Uma ferramenta para execução de contêineres Docker que simulam o funcionamento de um cluster Kubernetes. É utilizado para fins didáticos, de desenvolvimento e testes. O Kind não deve ser utilizado para produção;

Minikube: ferramenta para implementar um cluster Kubernetes localmente com apenas um nó. Muito utilizado para fins didáticos, de desenvolvimento e testes. O Minikube não deve ser utilizado para produção;

MicroK8S: Desenvolvido pela Canonical, mesma empresa que desenvolve o Ubuntu. Pode ser utilizado em diversas distribuições e pode ser utilizado em ambientes de produção, em especial para Edge Computing e IoT (Internet of things);

k3s: Desenvolvido pela Rancher Labs, é um concorrente direto do MicroK8s, podendo ser executado inclusive em Raspberry Pi;

k0s: Desenvolvido pela Mirantis, mesma empresa que adquiriu a parte enterprise do Docker. É uma distribuição do Kubernetes com todos os recursos necessários para funcionar em um único binário, que proporciona uma simplicidade na instalação e manutenção do cluster. A pronúncia é correta é kay-zero-ess e tem por objetivo reduzir o esforço técnico e desgaste na instalação de um cluster Kubernetes, por isso o seu nome faz alusão a Zero Friction. O k0s pode ser utilizado em ambientes de produção;



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
