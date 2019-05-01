---

copyright:
  years: 2017, 2019
lastupdated: "2019-03-13"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}

# Network Insights
{: #setup-network}

Com o {{site.data.keyword.security-advisor_long}}, é possível monitorar o comportamento usando o aprendizado de máquina, os padrões aprendidos e a inteligência de ameaça para detectar contêineres potencialmente comprometidos que são executados em seus clusters do {{site.data.keyword.containerlong_notm}}.
{: shortdesc}

A partir de 20 de janeiro de 2019, o Network Insights (beta) substitui o recurso Network Analytics. Todos os cartões de analítica em seu painel de serviço serão excluídos, mas as descobertas permanecerão no banco de dados de descobertas.
{: important}

## Antes de começar
{: #network-prereq}

Se você estiver atualmente usando o recurso Network Analytics, deverá [excluir os componentes de serviço](/docs/services/security-advisor?topic=security-advisor-setup-network#uninstall-analytics) antes de poder instalar o Network Insights. Para iniciar o Network Insights, certifique-se de que você tenha os pré-requisitos a seguir.

- Se você estiver trabalhando no Windows 10, ative o Windows Subsystem for Linux e instale um [shell do Ubuntu](https://win10faq.com/install-run-ubuntu-bash-windows-10/)
- Instale a CLI yq:
  * Para  [ macOS e Windows 10 ](http://mikefarah.github.io/yq/).
  * Para o CentOS, o Red Hat e o Ubuntu execute os comandos a seguir para instalar a versão 1.15.
    ```
    wget https://github.com/mikefarah/yq/releases/download/1.15.0/yq_linux_amd64       
    mv yq_linux_amd64 yq   
    chmod + x yq    
    mv yq /usr/local/bin/     
    yq -V
    ```
    {: codeblock}     
- Binário cURL atualizado: para o CentOS e o Red Hat, é possível atualizar executando `yum update -y nss curl libcurl`.
- A CLI do  [ {{site.data.keyword.cloud_notm}}  e plug-ins necessários ](/docs/cli?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli)
- A  [ CLI do Kubernetes ](https://kubernetes.io/docs/tasks/tools/install-kubectl/)  v1.10.11 ou superior
- O [Helm do Kubernetes (gerenciador de pacote)](/docs/containers?topic=containers-integrations#helm) v2.9.0 ou superior.
- Um cluster Kubernetes versão v1.10.11 ou superior

## Criando um bucket COS
{: #network-setup-cos}

Usando a GUI do {{site.data.keyword.security-advisor_short}}, é possível criar uma nova instância e depósito do COS.

1. Na guia **Integrações** do painel de serviço, alterne **Análise desativada** na caixa Network Insights para **Análise ativada**.

2. Clique em  ** Ir para a configuração **.

3. Na seção de pré-requisitos, clique em **Criar instância e depósito do COS**. A sua instância e o depósito do COS são criados automaticamente para você com a convenção de nomenclatura adequada e as permissões do IAM.

Se você tiver uma instância existente de COS e depósito, certifique-se de que ela use a convenção de nomenclatura: `sa.<account_id>.telemetric.<cos_region>`. Para permitir que o serviço leia os dados que estão armazenados em sua instância do COS, configure [autorização de serviço a serviço](/docs/iam?topic=iam-serviceauth#serviceauth) usando o {{site.data.keyword.cloud_notm}} IAM. Configure `source` como `{{site.data.keyword.security-advisor_short}}` e `target` como a sua instância do COS. Designe a função  ` Leitor `  do IAM.

## Instalando componentes do {{site.data.keyword.security-advisor_short}}
{: #network-install-components}

É possível instalar um agente para coletar logs de fluxo de rede por meio de seu cluster do Kubernetes. Os logs são armazenados em sua instância do Cloud Object Storage. É possível, então, ativar o Network Insights para analisar seus logs e detectar e alertá-lo sobre a atividade de rede suspeita.
{: shortdesc}

Certifique-se de repetir a instalação para cada cluster que você deseja monitorar.
{: note}

1. Clone o repositório a seguir para o seu sistema local.

  ```
  git clone https://github.com/ibm-cloud-security/security-advisor-network-insights.git
  ```
  {: codeblock}

2. Mude para a pasta `security-advisor-network-analytics`.

3. Extraia o arquivo `.tar` executando o comando a seguir.

  ```
  tar -xvf security-advisor-network-insights.tar
  ```
  {: codeblock}

4. Mude para a pasta  ` security-advisor-network-insights ` .

5. Efetue login na CLI do  {{site.data.keyword.cloud_notm}} . Siga os prompts na CLI para concluir a criação de log de conclusão.

  ```
  ibmcloud login -a https://api. < region> .bluemix.net
  ```
  {: codeblock}

  <table>
    <tr>
      <th>Região</th>
      <th>Nó de Extremidade</th>
    </tr>
    <tr>
      <td>Reino Unido</td>
      <td><code> eu-gb </code></td>
    </tr>
    <tr>
      <td>Sul dos EUA</td>
      <td><code> us-south </code></td>
    </tr>
  </table>

6. Configure o contexto para seu cluster.

  1. Obtenha o comando para configurar a variável de ambiente e fazer download dos arquivos de configuração do Kubernetes.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

  2. Copie a saída que começa com `export` e cole-a em seu terminal para configurar a variável de ambiente `KUBECONFIG`.

7. Instale o Helm usando os [docs de integração de Serviço do Kubernetes](/docs/containers?topic=containers-integrations#helm).

8. Opcional:  [ Ativar TLS ](https://github.com/helm/helm/blob/master/docs/tiller_ssl.md). Se você estiver usando a sua estação de trabalho para manipular a instalação de componentes de analítica em múltiplos clusters e o TLS estiver ativado, certifique-se de que as configurações do TLS sejam atuais e correspondam ao cluster atual no qual você planeja instalar os componentes.

9. Execute o comando a seguir para instalar o gráfico do Helm e suas dependências. O comando valida se o seu depósito usa a convenção de nomenclatura correta, cria segredos do Kubernetes, atualiza os valores com seu GUID do cluster e implementa o gráfico do Helm do Network Insights. Se você encontrar um erro, tente executar `helm init --upgrade`.

  ```
  ./network-insight-install.sh <cos_region> <cos_api_key>
  ```
  {: codeblock}

  <table>
    <tr>
      <th>Variável</th>
      <th>Descrição</th>
    </tr>
    <tr>
      <td><code> cos_region </code></td>
      <td>A região em que a sua instância do COS está implementada. As opções incluem:  <code> us-south </code>  e  <code> eu-gb </code>.</td>
    </tr>
    <tr>
      <td><code> cos_api_key </code></td>
      <td>A [chave de API](/docs/services/cloud-object-storage/iam?topic=cloud-object-storage-service-credentials#service-credentials) que você criou para acessar a sua instância e o depósito do COS. A chave deve ter a função de plataforma `writer`.</td>
    </tr>
  </table>

Você configurou com êxito seu cluster para funcionar com o {{site.data.keyword.security-advisor_short}} Network Insights!



## Excluindo os componentes
{: #network-delete}

Se você não precisar mais usar o Network Insights, será possível excluir os componentes de serviço de seu cluster.
{: shortdesc}

1. Efetue login na CLI do  {{site.data.keyword.cloud_notm}} . Siga os prompts na CLI para concluir a criação de log de conclusão.

  ```
  ibmcloud login -a https://api. < region> .bluemix.net
  ```
  {: codeblock}

  <table>
    <tr>
      <th>Região</th>
      <th>Nó de Extremidade</th>
    </tr>
    <tr>
      <td>Reino Unido</td>
      <td><code> eu-gb </code></td>
    </tr>
    <tr>
      <td>Sul dos EUA</td>
      <td><code> us-south </code></td>
    </tr>
  </table>

2. Configure o contexto para seu cluster.

  1. Obtenha o comando para configurar a variável de ambiente e fazer download dos arquivos de configuração do Kubernetes.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

  2. Copie a saída que começa com `export` e cole-a em seu terminal para configurar a variável de ambiente `KUBECONFIG`.

3. Exclua os componentes usando o Helm.

  ```
  helm del -- purge network-insights [ -- tls ]
  ```
  {: codeblock}

4. Exclua os segredos do Kubernetes.

  ```
  kubectl delete ns security-advisor-insights
  ```
  {: codeblock}

Certifique-se de excluir o processo para cada cluster do qual você deseja remover os agentes.
{: tip}

## Desinstalando o Network Analytics
{: #uninstall-analytics}

Se você usou a versão beta do Network Analytics, deverá desinstalar os componentes antigos do {{site.data.keyword.security-advisor_short}} antes de poder instalar os novos. Certifique-se de repetir esse processo para cada cluster que contiver quaisquer componentes de serviço.
{: shortdesc}

1. Efetue login no {{site.data.keyword.Bluemix_notm}}.

  ```
  ibmcloud login -a https://api.us-south.ibm.cloud.com -- sso
  ```
  {: pre}

2. Liste todos os clusters em sua conta para obter o nome do cluster.

  ```
  ibmcloud ks clusters
  ```
  {: pre}

3. Direcione sua CLI para o cluster.

  ```
  ibmcloud ks cluster-config <cluster-name-or-id>
  ```
  {: pre}

4. Configure o caminho para o arquivo local de configuração do Kubernetes como uma variável de ambiente. Exemplo:

  ```
  export KUBECONFIG=/Users/<user_name>/.bluemix/plugins/container-service/clusters/<cluster_name>/kube-config-prod-dal10-<cluster_name>.yml
  ```
  {: pre}

5. Navegue para a localização do archive extraído e execute o script desinstalador.

  ```
  ./uninstall.sh
  ```
  {: pre}

6. Opcional: desinstale do cluster o componente do servidor do Helm.

  ```
  helm reset
  ```
  {: pre}