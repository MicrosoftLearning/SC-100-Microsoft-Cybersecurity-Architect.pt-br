# Gerenciamento da superfície de ataque externa

## Visão geral do exercício

A Contoso visa aprimorar sua postura de segurança cibernética identificando e gerenciando sua superfície de ataque externa. Essa superfície inclui ativos hospedados em diferentes provedores de nuvem. Para atingir esse objetivo, a Contoso deseja integrar os dados da superfície de ataque ao Sentinel, a solução SIEM nativa de nuvem da empresa. Essa integração aprimorará os recursos de monitoramento de segurança e resposta a incidentes. 

## Parte 1: Criar uma solução (obrigatório)

Nesta tarefa, você criará um conceito para obter uma visão geral de seus ativos externos e sua superfície de ataque.

### Abordagem de design

A etapa inicial envolve análise dos requisitos com base no cenário descrito, entendendo-se os objetivos e a definição dos requisitos.

Com base no caso de uso em questão, os seguintes requisitos podem ser descritos:

- Os ativos externos da Contoso precisam ser monitorados e protegidos
- Descubra todos os ativos associados à Contoso
- Integre dados à solução SIEM da Contoso.
- Os ativos precisam ser gerenciados e rotulados

Na segunda etapa, examine o ambiente atual da Contoso Ltd. O GSAE (Gerenciamento da Superfície de Ataque Externa) do Microsoft Defender descobre e mapeia continuamente a superfície de ataque digital, fornecendo uma visão externa de uma infraestrutura online da organização. Ele identifica recursos expostos, prioriza riscos e estende o controle de vulnerabilidades e exposição além do firewall.

### Solução proposta

|Requisito|Solução|Plano de ação|
|----|----|----|
|Os ativos externos da Contoso precisam ser monitorados e protegidos| Defender EASM | Criar o recurso GSAE do Microsoft Defender|
|descubra todos os ativos associados à Contoso | Defender EASM |Criar um trabalho de descoberta nos ativos da Contoso  |
|Integrar dados à solução SIEM da Contoso |GSAE do Defender, Workspace do Log Analytics | Conectar o Workspace do Log Analytics ao GSAE do Defender |
|Os ativos precisam ser gerenciados e rotulados | Defender EASM | Gerenciar ativos e tags faturáveis |


## Parte 2: Implementar a solução (opcional)

### Tarefa 1 – Configurar o GSAE do Defender

Nesta tarefa, você criará um workspace do GSAE do Defender.

1. Faça logon na VM do Cliente 1 (LON-Sc1) como a conta **lon-sc1\admin** . A senha deve ser fornecida pelo seu provedor de hospedagem de laboratório.
1. Abra o **Microsoft Edge**, selecione a barra de endereços, navegue até **`https://portal.azure.com`** e faça logon no Portal do Azure como usuário.<user1-ZZZZZZZ@LODSUATMCA.onmicrosoft.com> A senha de administrador deve ser fornecida pelo seu provedor de hospedagem do laboratório.
1. Na caixa de diálogo Permanecer conectado?, selecione a caixa de seleção Não mostrar novamente e, em seguida, selecione Não.
1. Feche a caixa de diálogo de salvamento da senha na parte inferior selecionando **Nunca**, para não salvar as credenciais de administradores globais padrão em seu navegador.
1. Na barra de pesquisa superior, procure **`Microsoft Defender EASM`**.
1. Selecione **Criar**.
1. Em Criar Recurso GSAE do Microsoft Defender, selecione o grupo de recursos existente **rg_eastus_soc**.
    >[!NOTE] Se o grupo de recursos rg_eastus_soc não estiver listado, você precisará criá-lo novamente, pois a abertura de uma nova instância de laboratório não preserva o trabalho anterior.
1. Em Detalhes da instância, insira o nome **`EASM`**, selecione **Leste dos EUA** para a região.
1. Selecione **Examinar e Criar**.
1. Selecione **Criar**.

Você criou o workspace do GSAE do Defender.

### Tarefa 2 – Criar descoberta

Nesta tarefa, você criará uma descoberta sobre os ativos externos da na Contoso Ltd. Depois de criar uma instância, você precisa preenchê-la com dados reais. Portanto, agora você criará uma descoberta.

1. Você ainda deve estar conectado ao portal do Azure **https://portal.azure.com**.
1. Na barra de pesquisa na parte superior, pesquise e abra **`Microsoft Defender EASM`**.
1. Selecione o workspace **GSAE** que você criou na última tarefa.
1. Pesquise **Contoso** no campo de pesquisa **Pesquisar uma organização**.
1. Selecione **Contoso Ltd.**.
1. Selecione **Iniciar descoberta da superfície de ataque**.

Você criou a Descoberta da Superfície de Ataque Externa da Contoso e preencheu a instância do GSAE com dados acionáveis.

### Tarefa 3 – Configurar o conector de dados e o workspace do Log Analytics

Nesta tarefa, você configurará uma conexão de dados do GSAE do Defender para um workspace do Log Analytics que será usado para o Sentinel. As informações de ativos ou de insights do GSAE do Defender podem ser usadas no Log Analytics para enriquecer os fluxos de trabalho existentes com outros dados de segurança.

1. Você ainda deve estar conectado ao portal do Azure **https://portal.azure.com**.
1. Na barra de pesquisa na parte superior, procure **`Log Analytics Workspaces`**.
1. Selecione o seu workspace **law-sentinel** do último exercício.
    >[!NOTE] Se o workspace law-sentinel não estiver listado, você precisará criá-lo novamente, pois a abertura de uma nova instância de laboratório não preserva o trabalho anterior. Consulte o exercício do Centro de Operações de Segurança, parte 2, tarefa 1.
1. Deixe a página como está, abra outra guia e faça logon no portal do Azure **`https://portal.azure.com`**.
1. Na barra de pesquisa na parte superior, pesquise e abra **`Microsoft Defender EASM`**.
1. Selecione o workspace do **GSAE**.
1. No painel de navegação esquerdo, expanda **Gerenciar** e selecione **Conexões de dados**.
1. Em Log Analytics, selecione **Adicionar conexão**.
1. Nomeie-o **law-sentinel**
1. Alterne para a guia anterior com o workspace do Log Analytics que deve estar aberto.
1. Expanda **Instruções do agente do Log Analytics**.
1. Copie a **ID do workspace** no campo correspondente da janela Adicionar conexão de dados.
1. Copie a ****Chave primária** no campo Chave de API da janela Adicionar conexão de dados.
1. Em Conteúdo, selecione **Tudo**.
1. Em Frequência, selecione **Diariamente**.
1. Selecione **Adicionar**.
1. O cartão do Log Analytics da página Conexões de dados mostrará law-sentinel, listado em Conectado (1).

Depois que a conexão for criada, as tabelas de log personalizadas serão criadas no workspace do Log Analytics. No Sentinel, esses dados podem ser usados para criar ou enriquecer incidentes de segurança, criar manuais de investigação, treinar algoritmos de aprendizado de máquina ou acionar ações de correção.

Você configurou a conexão entre o GSAE do Defender e um workspace do Log Analytics.

### Tarefa 4 – Revisar painéis e rotular ativos

Nesta tarefa, você examinará a postura de segurança do GSAE do Defender e obterá informações sobre descobertas.

1. Você ainda deve estar conectado ao portal do Azure **https://portal.azure.com**.
1. Na barra de pesquisa na parte superior, pesquise e abra **`Microsoft Defender EASM`**.
1. Selecione o workspace do **GSAE**.
1. No painel de navegação esquerdo, expanda **Painéis** e selecione **Resumo da superfície de ataque**. Os painéis de Resumo da Superfície de Ataque fornecem insights importantes e uma visão geral de alto nível dos principais ativos afetados de sua superfície de ataque.
1. Revise o painel **Resumo da superfície de ataque**.
1. No painel de navegação esquerdo, clique em **Postura de segurança**.
1. Revise as diferentes categorias de vulnerabilidades abertas.
1. Na categoria **Portas abertas**, selecione **Servidores Web**.
1. Selecione o endereço IP encontrado **34.223.124.45**.
1. Você decide rotular o ativo para uma investigação mais aprofundada.
1. Selecione **Modificar ativo**.
1. Selecione **Criar novo rótulo**.
1. Nomeie-o como **Portas abertas** e selecione **Adicionar**.
1. Atribua o rótulo recém-criado no campo **Rótulos**.
1. Selecione **Atualizar**.

Você revisou a Postura de segurança e rotulou um ativo para investigação adicional.

### Tarefa 5 – Gerenciar ativos

Nesta tarefa, você gerenciará e categorizará os ativos descobertos.

1. Você ainda deve estar conectado ao portal do Azure **https://portal.azure.com**.
1. Na barra de pesquisa na parte superior, pesquise e abra **`Microsoft Defender EASM`**.
1. Selecione o workspace do **GSAE**.
1. No painel de navegação esquerdo, expanda **Geral** e selecione **Estoque**.
1. Na página GSAE | Estoque, a guia Pesquisar está selecionada (sublinhada). No campo de pesquisa, use o menu suspenso para selecionar **Rótulos**
1. No menu suspenso abaixo, escolha o rótulo que você criou recentemente, **Portas abertas**.
1. Selecione **Pesquisar**.
1. Abra o ativo encontrado **34.223.124.45**.
1. Selecione a guia **Componentes da Web**.
1. Você identificou que esse ativo está hospedado na Amazon, também há CVEs abertos em alguns dos componentes, mas eles não estão ativos, como você pode ver na coluna **Recentes** e **Última aparição**. Eles se originam de execuções de descoberta anteriores.
Como esse ativo é hospedado por terceiros, mas ainda pertence à sua superfície de ataque, você o categoriza com base na função dele em sua organização.
1. Selecione **Modificar ativo**.
1. Na janela Modificar ativo, use o campo suspenso **Estado** para selecionar **Dependência**.
1. Selecione **Atualizar**.
    >[!NOTE]Nesse caso, escolha Dependência, porque o ativo é uma infraestrutura que pertence a terceiros, mas que faz parte da superfície de ataque já que dá suporte diretamente à operação de seus ativos.
1. Volte para o Estoque clicando no **X** no canto superior direito e crie uma nova Pesquisa.
1. Modifique a consulta de pesquisa para **Nome do componente da Web — contém — Amazon**.
1. Selecione **Pesquisar**.
1. Selecione todos os Ativos.
1. Selecione **Modificar ativos**.
1. Escolha **Dependência** em Estado e selecione **Atualizar**.

Somente se o Estado estiver definido como **Estoque aprovado**, os ativos serão representados em gráficos de painel e serão verificados diariamente. Por esse motivo, é importante revisar os ativos recém-descobertos e alterar os respectivos estados de acordo.

Como parte deste exercício, você configurou o GSAE do Defender, criou a descoberta do ambiente externo da Contoso, obteve uma visão mais detalhada dos ativos e sua configuração e gerenciou ativos para que os painéis incluam apenas dados pelos quais a Contoso é diretamente responsável.
