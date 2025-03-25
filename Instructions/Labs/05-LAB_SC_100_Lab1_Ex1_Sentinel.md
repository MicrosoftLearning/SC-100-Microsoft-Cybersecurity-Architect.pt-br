# Centro de Operações de Segurança

## Visão geral do exercício

A Contoso tem um SOC (Centro de Operações de Segurança) que monitora e responde a incidentes de segurança em toda a empresa. O SOC é composto por analistas de segurança, engenheiros de segurança e engenheiros de rede. O SOC decidiu usar o Microsoft Sentinel como solução de SIEM (Gerenciamento de Eventos e Informações de Segurança). Para coletar e analisar logs de segurança de toda a empresa, o SOC tem um workspace do Log Analytics. O SOC tem um requisito para proteger o acesso ao workspace do Log Analytics com base no princípio de privilégios mínimos. O SOC tem duas funções diferentes, analista de segurança e engenheiro de segurança, com diferentes requisitos de permissão. A equipe de rede tem o requisito de acessar apenas os registros do Cisco Umbrella.

## Parte 1: Criar uma solução (obrigatório)

Nesta tarefa, você criará um conceito para monitorar e responder a eventos de segurança com permissões de acesso específicas para o Centro de Operações de Segurança da Contoso.

### Abordagem de design

A etapa inicial envolve a análise dos requisitos com base no cenário descrito, a compreensão dos objetivos e a definição dos requisitos.

Com base no caso de uso fornecido, os seguintes requisitos podem ser descritos:

- Implantar solução SIEM/SOAR
- Limitar o acesso a funções específicas do SOC
- Criar um painel com exibições personalizadas para incidentes e seus alertas

Nesse cenário, você implantará a solução SOAR do SIEM com base no Microsoft Sentinel, configurará o controle de acesso baseado em função no contexto do workspace e limitará o acesso da equipe de rede a uma única tabela no workspace do Log Analytics. As pastas de trabalho permitem que analistas e administradores de segurança visualizem dados de segurança usando exibições gráficas. Elas fornecem uma ferramenta para apresentar e analisar dados em um painel.

### Solução proposta

| Requisito | Solução | Plano de ação |
| ---- | ---- | ---- |
| Implantar solução SIEM/SOAR | Microsoft Sentinel, Workspace do Log Analytics | Configurar o workspace do Log Analytics e implantar o Microsoft Sentinel |
| Limitar o acesso a funções específicas do SOC | Workspace do Log Analytics, Controle de acesso baseado em função | Configurar o RBAC para o Workspace do Log Analytics |
| Criar um painel com exibições personalizadas para incidentes e seus alertas | Microsoft Sentinel, Pasta de trabalho | Criar uma pasta de trabalho com uma exibição personalizada sobre incidentes e alertas atuais |

## Parte 2: Implementar a solução (opcional)

> [!NOTE]
> Para esta parte do laboratório, a tarefa de criar um painel com exibições personalizadas para incidentes e seus respectivos alertas (tarefa 4 deste exercício) não é funcional, pois não há dados a serem usados para executar essa tarefa. As etapas da tarefa 4 são incluídas apenas para fins informativos. A execução das etapas não retornará nenhum dado.

### Tarefa 1 — Criar um workspace do Log Analytics

Nesta tarefa, você criará um workspace do Log Analytics, que é necessário para hospedar todos os dados que o Microsoft Sentinel ingerirá e usará para as detecções, análises e outros recursos.

1. Faça logon na VM do Cliente 1 (LON-SC1) como a conta **lon-sc1\admin**. A senha deve ser fornecida pelo seu provedor de hospedagem de laboratório.
2. Abra o **Microsoft Edge**, selecione a barra de endereços, navegue até **`https://portal.azure.com`** e faça logon no Portal do Azure como usuário **User1-*******@LODSUATMCA.onmicrosoft.com** (em que ****** é sua ID de locatário exclusiva fornecida pelo seu provedor de hospedagem de laboratório). A senha do usuário deve ser fornecida pelo provedor de hospedagem do laboratório.
3. Na caixa de diálogo "Permanecer conectado?", selecione a caixa de seleção "Não mostrar novamente" e, em seguida, selecione **Não**.
4. Feche a caixa de diálogo de salvamento de senha na parte inferior selecionando "Nunca" para não salvar as credenciais de administradores globais padrão em seu navegador.
5. Cancele a tela de Boas-vindas ao Microsoft Azure.
6. Selecione **Criar recurso** e procure por **workspace do Log Analytics**
7. Encontre o **bloco Workspace do Log Analytics** e selecione **Criar**.
8. No espaço "Criar workspace do Log Analytics", crie um novo **Grupo de recurso** e atribua o nome **`rg_eastus_soc`**.
9. Em Detalhes da instância, insira o nome **`law-sentinel`**, selecione **Leste dos EUA** para a região.
10. Selecione **Revisar e criar**
11. Selecione **Criar** para iniciar a implantação.

Você criou o workspace do Log Analytics para sua implantação do Sentinel.

### Tarefa 2 – Criar o Sentinel

Nesta tarefa, você adicionará o Sentinel ao workspace do Log Analytics criado.

1. Você ainda deve estar conectado ao portal do Azure **https://portal.azure.com**.
1. Na barra de pesquisa, na faixa azul na parte superior da página, insira **Microsoft Sentinel** e selecione-o nos resultados da pesquisa listados em serviços.
1. Na página do **Microsoft Sentinel**, selecione **Criar**.
1. Na página **Adicionar um Microsoft Sentinel a um workspace**, o workspace do Log Analytics criado anteriormente estará listado.  Selecione **law-sentinel** e **Adicionar**.
1. Pode levar alguns minutos para adicionar o Sentinel ao workspace.  Depois de adicionado, a página **Microsoft Sentinel | Notícias e Guia**s será exibida.  Você receberá uma notificação de que a avaliação gratuita do Microsoft Sentinel está ativada.  Selecione **OK**.
1. No centro da página, selecione **Ir para o hub de conteúdo**.  O hub de conteúdo é onde você baixa soluções. Fique à vontade para explorar hub de conteúdo.

Você implantou o Sentinel no workspace do Log Analytics. 

### Tarefa 3 – Configurar o RBAC

Você precisa proteger o acesso com base no privilégio mínimo e criará atribuições de função para os requisitos de função específicos. Em sua próxima implantação produtiva, haverá duas funções diferentes no Centro de Operações de Segurança.


#### Requisitos de permissão

| Função | Permissões |
|---|---|
| Analista de segurança | Exibir dados, incidentes, pastas de trabalho e outros recursos do Sentinel e Atribuir/descartar incidentes. |
| Engenheiro de segurança | Criar e editar pastas de trabalho e regras de análise — Instalar e atualizar soluções no hub de conteúdo |

---

1. Você ainda deve estar conectado ao portal do Azure **https://portal.azure.com**.
1. Na barra de pesquisa superior, pesquise **Grupos de recursos** e selecione o grupo de recursos criado anteriormente **rg_eastus_soc**.
1. No painel de navegação à esquerda, selecione **Controle de acesso (IAM)**.
1. Selecione **Adicionar** e, no menu suspenso, selecione **Adicionar atribuição de função**.
1. Pesquise **`Microsoft Sentinel Responder`** e selecione **Exibir** na coluna Detalhes.
1. Verifique se as permissões correspondem aos requisitos.
1. Feche a janela clicando no **X** no canto superior direito.
1. Selecione **Avançar**.
1. Selecione **+Selecionar membros**.
1. Pesquise o Grupo **`SOC Analysts`**, selecione **Analistas do SOC** nos resultados da pesquisa, aperte **Selecionar** e adicione a atribuição de função.
1. Selecione **Examinar + atribuir**.
1. Você repetirá as etapas para a função Colaborador do Sentinel. Selecione **Adicionar** e, no menu suspenso, selecione **Adicionar atribuição de função**.
1. Pesquise **`Microsoft Sentinel Contributor`** e selecione a função.
1. Selecione **Avançar**.
1. Selecione **+Selecionar membros**.
1. Na folha **Selecionar membros**, pesquise o Grupo **Engenheiros do SOC**.  Nos resultados da pesquisa, selecione **Engenheiros do SOC** e pressione **Selecionar** para adicionar a atribuição de função.
1. Selecione **Revisar + atribuir** novamente.
1. Selecione a guia **Atribuições de função** e confirme se as atribuições de função estão definidas.

Você criou o modelo de acesso baseado em função para os requisitos de função da equipe de operações de segurança da Contoso.

### Tarefa 4 — Criar uma pasta de trabalho

> [!NOTE]
> Essas etapas são incluídas apenas para fins informativos. A execução das etapas não retornará nenhum dado.

Nesta tarefa, você criará uma pasta de trabalho para obter um painel com exibições personalizadas e incidentes atuais e seus alertas.

1. Você ainda deve estar conectado ao portal do Azure **https://portal.azure.com**.
1. Na barra Pesquisa na parte superior, pesquise e abra **`Microsoft Sentinel`**.
1. Selecione **law-sentinel**.
1. No painel de navegação esquerdo, expanda **Gerenciamento de ameaças** e selecione **Pastas de trabalho**.
1. Selecione **Adicionar pasta de trabalho**.
1. Selecione **Editar**.
1. Selecione o primeiro botão **Editar** no lado direito.
1. Selecione **Adicionar** > **Adicionar parâmetros**.
1. Selecione **Adicionar parâmetro** e preencha as seguintes informações:
     - **Nome do parâmetro:** TimeRange
     - **Tipo de parâmetro**: Seletor de intervalo de tempo
1. Verifique as seguintes configurações:
     - **Obrigatório?**
1. Selecione **Salvar**.
1. No menu suspenso **TimeRange:** no canto inferior esquerdo, selecione **Últimos 7 dias**.
1. Selecione **Adicionar parâmetro** e preencha as seguintes informações:
     - **Nome do parâmetro:** AlertSeverity
     - **Tipo de parâmetro:** menu suspenso
1. Verifique as seguintes configurações:
     - **Obrigatório?**
     - **Permitir várias seleções**
     - **Ocultar o parâmetro no modo de leitura**
1. Em **Consulta de logs do workspace do Log Analytics**, cole:

    ```KQL
    SecurityAlert
    | summarize Count = count() by AlertSeverity
    | order by Count desc, AlertSeverity
    | project Value = AlertSeverity, Label = strcat(AlertSeverity, ' - ', Count)
    ```

1. No menu suspenso **Intervalo de tempo**, selecione **TimeRange**.
1. Role para baixo até **Incluir no menu suspenso**, marque **Todos** e defina o **Item selecionado padrão** como **Todos**.
1. Selecione **Salvar**.
1. Selecione **Adicionar parâmetro** e preencha as seguintes informações:
     - **Nome do parâmetro:** ProductName
     - **Tipo de parâmetro:** menu suspenso
1. Verifique as seguintes configurações:
     - **Obrigatório?**
     - **Permitir várias seleções**
     - **Ocultar o parâmetro no modo de leitura**

1. Em **Consulta de logs do workspace do Log Analytics**, cole:

    ```KQL
    SecurityAlert
    | summarize Count = count() by ProductName
    | order by Count desc, ProductName asc
    | project Value = ProductName, Label = strcat(ProductName, ' - ', Count)
    ```

1. No menu suspenso **Intervalo de tempo**, selecione **TimeRange**
1. Role para baixo até **Incluir no menu suspenso**, marque **Todos** e defina o **Item selecionado padrão** como **Todos**.
1. Selecione **Salvar**.
1. Selecione **Adicionar** e **Adicionar consulta**.
1. Em **Consulta de logs do workspace do Log Analytics**, cole:

    ```KQL
    SecurityIncident
    | where CreatedTime {TimeRange:value}
    | summarize arg_max(TimeGenerated,*) by tostring(IncidentNumber)
    | extend IncidentID = IncidentName
    | extend Alerts = extract("\\[(.*?)\\]", 1, tostring(AlertIds))
    | mv-expand AlertIds to typeof(string)
    | join
    (
        SecurityAlert
        | extend AlertEntities = parse_json(Entities)
        | mv-expand AlertEntities
    ) on $left.AlertIds == $right.SystemAlertId
    | summarize AlertCount=dcount(AlertIds) by IncidentNumber, Status, Severity, Title, Alerts, IncidentUrl, IncidentID
    | project IncidentNumber, IncidentID, Title, Severity, Status, AlertCount, Alerts, IncidentUrl
    | order by Severity
    ```

1. Escolha **TimeRange** no menu suspenso Intervalo de Tempo.
Você configurará o conteúdo dinâmico para obter todos os alertas para o incidente selecionado. Os alertas serão exportados e estarão disponíveis fora dessa consulta.
1. Selecione a guia **Configurações avançadas** na parte superior da janela **Edição de consulta**.
1. Verifique as seguintes configurações:
    - **Quando os itens estiverem selecionados, exportar os parâmetros** 
1. Selecione **Adicionar Parâmetro** e preencha as seguintes informações:
    - **Campo a ser exportado:** Alertas
    - **Nome do parâmetro:** Alertas
1. Selecione **Salvar**.
1. Retorne à guia **Configurações**.
1. Selecione **Executar Consulta**.
1. Selecione **Configurações de Coluna**.
1. Selecione **IncidentUrl**.
1. Defina o renderizador de coluna como **Link**.
1. Em Configurações de link, defina **Exibir para abrir** como **URL**.
1. Selecione **Salvar e Fechar**.
1. Em seguida, você criará a exibição de alertas com base em qual incidente está selecionado.
1. Selecione **+ Adicionar** na parte inferior da janela **Edição do item de consulta**. Selecione **Adicionar consulta**.
1. Cole o KQL na Consulta de logs do workspace do Log Analytics

    ```KQL
    SecurityAlert
    | where SystemAlertId in ({Alerts})
    | summarize by  DisplayName, StartTime, EndTime,  SystemAlertId
    | sort by EndTime desc
    ```

1. Escolha **TimeRange** no menu suspenso Intervalo de tempo.
1. Selecione **Done Editing**.
1. Selecione **Edição concluída** na barra superior da janela **Nova pasta de trabalho**.
1. Selecione um **Incidente**.
1. Alertas para o incidente vinculado aparecerão abaixo.
1. Salve a consulta selecionando o ícone Salvar.  
1. Na janela **Salvar como**, insira um título para sua nova pasta de trabalho, selecione o grupo de recursos **rg_eastus_soc** na lista suspensa e selecione **Salvar como**.

Você criou um painel com exibições personalizadas para incidentes e os alertas associados.
