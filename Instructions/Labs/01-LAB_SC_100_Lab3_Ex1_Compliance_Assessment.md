# Avaliação de conformidade

## Introdução ao cenário do laboratório

Você é Allan Deyoung, membro do departamento de TI da Contoso Ltd. Você foi transferido recentemente para a divisão de segurança de TI. Sua nova função é avaliar a prontidão de Confiança Zero da Contoso e desenvolver um plano de ação para estabelecer uma iniciativa de Confiança Zero, seguindo os pilares de Confiança Zero. A Contoso é uma grande corporação multinacional com presença global em vários setores. A empresa tem um grande volume na nuvem e uma infraestrutura híbrida. O SOC (centro de operações de segurança) da Contoso é responsável por monitorar e responder a incidentes de segurança em toda a empresa. O SOC é composto por analistas de segurança, engenheiros de segurança e engenheiros de rede. O SOC usa o Microsoft Sentinel como sua solução de SIEM (gerenciamento de eventos e informações de segurança). O SOC tem um workspace do Log Analytics que é usado para coletar e analisar logs de segurança de toda a empresa.

A Contoso Ltd. está se expandindo para a Europa para aumentar as vendas, mas está tendo problemas para atender às demandas de segurança de TI dos clientes. Os clientes querem que a Contoso mantenha um ambiente protegido para facilitar a colaboração segura e minimizar o risco de vazamentos de dados e ativos comprometidos da empresa. Muitos clientes exigem evidências de processos empresariais de TI bem estabelecidos e uma estrutura de segurança robusta, que geralmente está na forma de uma certificação ISO-27001. Para resolver isso, a Contoso decidiu contratar uma empresa de auditoria externa para realizar a auditoria ISO-27001 e obter a certificação. É necessário avaliar a postura organizacional atual e desenvolver um plano de ação para atender aos requisitos da ISO-27001. Como arquiteto de segurança cibernética da empresa, você tem a tarefa de identificar as lacunas existentes e atribuir tarefas específicas às pessoas dentro da organização para resolvê-las.

## Parte 1: Criar uma solução (obrigatório)

Nesta tarefa, você criará um conceito para resolver os desafios que a Contoso Ltd. está enfrentando.

### Abordagem de design

Para resolver o problema descrito de forma eficaz, é crucial entender a ISO 27001 completamente. Avaliar a configuração da Contoso em relação aos padrões ISO 27001 é essencial, destacando quaisquer inconsistências para análise. Esse processo pode ser demorado devido à complexidade do ambiente M365 e dos regulamentos do 27001. No entanto, a avaliação do Gerenciador de Conformidade da Microsoft simplifica essa análise.

As avaliações do Gerenciador de Conformidade da Microsoft são agrupamentos de controles de políticas, padrões ou regulamentos específicos. Elas ajudam a garantir que sua organização atenda aos requisitos de vários padrões, regulamentos ou leis. Por exemplo, concluir todas as ações em uma avaliação pode alinhar as configurações do Microsoft 365 com os requisitos da ISO 27001. As avaliações abrangem vários componentes e fornecem modelos para mais de 360 regulamentos, oferecendo os controles e etapas necessários para avaliar sua conformidade de forma eficaz. 

### Solução Proposta

|Requisito|Solução|Plano de ação|
|----|----|----|
|Comparação do ambiente M365 com os regulamentos ISO 27001|Gerenciador de Conformidade do Microsoft Purview|Criar uma avaliação|
|Criar um plano de ação|Gerenciador de Conformidade do Microsoft Purview|Atribuir tarefas a um engenheiro técnico|

## Parte 2: Implementar a solução (opcional)

### Tarefa 1: Realizar uma avaliação da ISO-27001

Seu primeiro passo é analisar o ambiente atual da empresa. Você realiza uma avaliação de conformidade para analisar até que ponto o ambiente da Contoso está em conformidade com os regulamentos ISO-27001.

1. Entre no portal de Conformidade do Microsoft Purview**`https://purview.microsoft.com/`** como Allan Deyoung usando sua conta de **Administrador MOD**.
1. Se você for solicitado a configurar a autenticação multifator, siga as instruções.
1. Você é levado para a nova página de aterrissagem do portal do Microsoft Purview. Selecione a caixa ao lado da frase “**Eu concordo com os termos de divulgação de fluxo de dados e políticas de privacidade**”, e depois selecione **Começar**.
1. No painel de navegação à esquerda, selecione **Soluções**, e depois selecione **Gerenciador de Conformidade**. Como alternativa, na janela principal, você pode selecionar o bloco **Exibir todas as soluções** e, em seguida, selecionar o bloco **Gerenciador de Conformidade** listado em Risco e Conformidade.
1. No painel **Gerenciador de Conformidade** à esquerda, selecione **Avaliações**.
1. Na janela **Avaliações** , selecione **+ Adicionar avaliação**.
1. Na janela **Basear sua avaliação em um regulamento**, selecione **Selecionar regulamento**.
1. Na caixa de texto de pesquisa, digite **`ISO/IEC 27001:2022`**, selecione o regulamento, **Salvar** e, em seguida, **Avançar**.
1. Na página **Adicionar nome e grupo**, na caixa de texto **Nome da avaliação** , digite **`ISO-27001 Audit assessment`**. Deixe a configuração do **Grupo de avaliação** como **Usar o grupo atual** com o **Grupo padrão** e selecione **Avançar**.
1. Na página **Selecionar serviços** , o serviço do **Microsoft 365** já deve estar listado.  Caso contrário, selecione **Selecionar serviços**, **Microsoft 365** e, em seguida, **Adicionar**. Selecione **Avançar**.
1. Na página **Revisar e concluir**, selecione **Criar a avaliação**. Levará alguns segundos para criar a avaliação. Em seguida, selecione **Concluído**.
1. Agora você acessará a página de **Avaliação de auditoria ISO-27001** recém-criada.
1. Deixe esta guia do navegador aberta para a próxima tarefa.

Você criou uma avaliação com base na ISO-27001.

### Tarefa 2: Atribuir tarefas a um engenheiro técnico

Os resultados da avaliação mostram diferentes áreas e ações que são essenciais para cumprir os regulamentos da ISO-27011. Você investigará ações de melhoria e atribuirá uma tarefa a um engenheiro técnico.

1. Você ainda deve estar na página da avaliação que acabou de criar, **Avaliação de auditoria ISO-27001**.  Caso contrário, navegue até o portal do Microsoft Purview **`https://purview.microsoft.com/`** e, a partir daí, selecione **Soluções** > **Gerenciador de Conformidade** > **Avaliações** > **Avaliação de auditoria ISO-27001**
1. Na página **Avaliação de auditoria ISO-27001**, selecione **Suas ações de melhoria**.
1. Defina o filtro de **Família de controle** como **Controles físicos**.
1. Marque a caixa ao lado de **Ação de melhoria** para selecionar todas as ações de melhoria mostradas e, em seguida, selecione **Atribuir ao usuário** (listado acima das opções de filtros).
1. Na nova janela **Atribuir ações de melhoria**, na caixa de texto de pesquisa, digite **`Nestor`** e pressione Enter.
1. Selecione o usuário e, em seguida, **Atribuir**.
1. Deixe esta guia do navegador aberta para a próxima tarefa.

Você visualizou e atribuiu uma ação de melhoria a um engenheiro técnico

### Tarefa 3: Fornecer acesso a um engenheiro técnico para as ações de melhoria

Os usuários precisam de acesso para visualizar as tarefas atribuídas a eles. Você concederá a Nestor Wilke acesso à avaliação.

1. Você ainda deve permanecer na guia **Suas ações de melhoria** na página **Avaliação de auditoria ISO-27001**.  Caso contrário, navegue até o portal do Microsoft Purview **`https://purview.microsoft.com/`** e, a partir daí, selecione **Soluções** > **Gerenciador de Conformidade** > **Avaliações** > **Avaliação de auditoria ISO-27001** > **Suas ações de melhoria**.
1. No canto superior direito da página **Avaliação ISO/IEC 27001:**, selecione **Gerenciar acesso do usuário**.
1. Na nova janela **Gerenciar acesso do usuário**, selecione a guia **Avaliador** e, em seguida, **Adicionar avaliadores**.
1. Na caixa de texto **Pesquisar**, digite **`Nestor`** e pressione Enter.
1. Selecione o usuário e, em seguida, **Aplicar**. Feito isso, selecione **Salvar**.
1. Você concedeu a Nestor Wilke a função de Avaliador dessa avaliação.
1. Você já pode sair do portal do Microsoft Purview fechando a guia do navegador.

Você concedeu a Nestor Wilke a função de Avaliador dessa avaliação.
