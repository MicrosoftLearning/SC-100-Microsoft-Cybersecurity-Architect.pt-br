# Laboratório 1 — Exercício 1 — Centro de Operações de Segurança

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

### Tarefa 1 — Criar um workspace do Log Analytics

Nesta tarefa, você criará um workspace do Log Analytics, que é necessário para hospedar todos os dados que o Microsoft Sentinel ingerirá e usará para as detecções, análises e outros recursos.

1. Faça logon na VM do Cliente 1 (LON-SC1) como a conta **lon-sc1\admin**. A senha deve ser fornecida pelo seu provedor de hospedagem de laboratório.
2. Abra o **Microsoft Edge**, selecione a barra de endereços, navegue até **https://portal.azure.com** e faça logon no Portal do Azure como usuário **User1-*******@LODSUATMCA.onmicrosoft.com** (em que ****** é sua ID de locatário exclusiva fornecida pelo seu provedor de hospedagem de laboratório). A senha do usuário deve ser fornecida pelo provedor de hospedagem do laboratório.
3. Na caixa de diálogo "Permanecer conectado?", selecione a caixa de seleção "Não mostrar novamente" e, em seguida, selecione **Não**.
4. Feche a caixa de diálogo de salvamento de senha na parte inferior selecionando "Nunca" para não salvar as credenciais de administradores globais padrão em seu navegador.
5. Cancele a tela de Boas-vindas ao Microsoft Azure.
6. Selecione **Criar recurso** e procure por **workspace do Log Analytics**
7. Encontre o **bloco Workspace do Log Analytics** e selecione **Criar**.
8. Em Criar site do workspace do Log Analytics, crie um novo **Grupo de recursos** e nomeie-o **rg_eastus_soc**.
9. Em Detalhes da instância, insira o nome **law-sentinel** e selecione **Leste dos EUA** em região.
10. Selecione **Revisar e criar**
11. Selecione **Criar** para iniciar a implantação.

Você criou o workspace do Log Analytics para sua implantação do Sentinel.

### Tarefa 2 – Criar o Sentinel

Nesta tarefa, você adicionará o Sentinel ao workspace do Log Analytics criado e adicionará logs de demonstração; como o locatário de demonstração não tem dados existentes no workspace do Log Analytics, você importará logs de demonstração para ter uma ideia melhor de como o Sentinel funciona.

1. Você ainda deve estar conectado ao portal do Azure **https://portal.azure.com**.
2. Selecione **Criar um recurso** e pesquise **Microsoft Sentinel**, Filtrar por **Tipo de Produto: Serviços do Azure**.
3. Encontre o **bloco do Microsoft Sentinel** e selecione **Criar**.
4. Selecione **Adicionar** e busque o workspace do Log Analytics criado anteriormente **law-sentinel**.
5. Confirme clicando em **Adicionar**.
6. No painel de navegação esquerdo, selecione **Hub de conteúdo**.
7. Pesquise **Laboratório de Treinamento do Microsoft Sentinel**, **selecione** e **instale** a solução.
8. Selecione **Criar**.
9. Escolha o grupo de recursos **rg_eastus_soc** e o workspace **law-sentinel**.
10. Selecione **Examinar e Criar**.
11. Confirme a implantação **Criar**.
12. Aguarde a instalação da solução.

Você implantou o Sentinel no workspace do Log Analytics e adicionou dados. 

### Tarefa 3 – Configurar o RBAC

Você precisa proteger o acesso com base no privilégio mínimo e criará atribuições de função para os requisitos de função específicos. Em sua próxima implantação produtiva, haverá duas funções diferentes no Centro de Operações de Segurança.
Além disso, a equipe de rede precisa acessar os registros da Cisco Umbrella. Você deve garantir que a equipe de rede só possa acessar esses logs.

#### Requisitos de permissão

| Função | Permissões |
|---|---|
| Analista de segurança | Exibir dados, incidentes, pastas de trabalho e outros recursos do Azure Sentinel |
| | Atribuir/descartar incidentes. |
| Engenheiro de segurança | Criar e editar pastas de trabalho e regras de análise |
| | Instalar e atualizar soluções no hub de conteúdo |
| Equipe de rede | Permissões de leitura para grupo: **NOC** na tabela: **Cisco_Umbrella_dns_CL**|

---

1. Você ainda deve estar conectado ao portal do Azure **https://portal.azure.com**.
2. Na barra de pesquisa superior, pesquise **Grupos de recursos** e selecione o grupo de recursos criado anteriormente **rg_eastus_soc**.
3. No painel de navegação à esquerda, selecione **Controle de acesso (IAM)**.
4. Selecione **Adicionar** e, no menu suspenso, selecione **Adicionar atribuição de função**.
5. Pesquise o **Respondente do Microsoft Sentinel** e selecione **Exibir** na coluna Detalhes.
6. Verifique se as permissões correspondem aos requisitos.
7. Feche a janela clicando no **X** no canto superior direito.
8. Selecione **Avançar**.
9. Selecione **+Selecionar membros**.
10. Pesquise o Grupo de **Analistas SOC** e adicione a atribuição de função.
11. Selecione **Examinar + atribuir**.
12. Selecione **Adicionar** e, no menu suspenso, selecione **Adicionar atribuição de função**.
13. Pesquise **Colaborador do Microsoft Sentinel** e selecione a função.
14. Selecione **Avançar**.
15. Selecione **+Selecionar membros**.
16. Na folha **Selecionar membros**, pesquise o Grupo de **Engenheiros do SOC** e **selecione** a atribuição de função.
17. Selecione **Revisar + atribuir** novamente.
18. Selecione a guia **Atribuições de função** e confirme se as atribuições de função estão definidas.
19. No menu suspenso, selecione **Adicionar** e **Adicionar função personalizada**.
20. Nomeie **NOC-CiscoUmbrellaCL-Read**.
21. Em **Permissão de linha de base**, selecione **Iniciar do zero**.
22. Selecione **Avançar**.
23. Na guia **Permissões**, selecione **Adicionar permissões**.
24. Pesquise **Microsoft.OperationalInsights** e selecione o cartão de **Análise de Log do Azure**.
25. Adicione as seguintes permissões.

```
Microsoft.OperationalInsights/workspaces
Read : Get Workspace
Other : Search Workspace Data

Microsoft.OperationalInsights/workspaces/analytics
Other : Search 

Microsoft.OperationalInsights/workspaces/query
Read : Query Data in Workspace 

Microsoft.OperationalInsights/workspaces/tables/query
Read : Query workspace table data 
```

26.  Selecione **Examinar + criar**.
27. Selecione **Criar**.
28. Na barra de pesquisa superior, pesquise **Grupos de recursos** e selecione **rg_eastus_soc**.
29. Abra o workspace do Log Analytics **law-sentinel**.
30. No painel de navegação esquerdo, expanda **Configurações** e selecione **Tabelas**.
31. Pesquise **Cisco_Umbrella_dns_CL**.
32. Clique nas reticências (...), selecione **Controle de acesso (IAM).**
33. Selecione **Adicionar** > **Adicionar atribuição de função**.
34. Procure por **NOC-CiscoUmbrellaCL-Read** e selecione a função personalizada.
35. Selecione Avançar.
36. Selecione **Selecionar membros**, pesquise NOC e **selecione** o grupo.
37. Selecione **Examinar + atribuir**.

Você criou o modelo de acesso baseado em função para os requisitos de função da equipe de operações de segurança da Contoso e criou uma função personalizada para a equipe de rede, além de ter atribuído a função na tabela específica em seu workspace do Log Analytics.

### Tarefa 4 — Criar uma pasta de trabalho

Nesta tarefa, você criará uma pasta de trabalho para obter um painel com exibições personalizadas e incidentes atuais e seus alertas.

1. Você ainda deve estar conectado ao portal do Azure **https://portal.azure.com**.
2. Na barra de pesquisa na parte superior, pesquise e abra o **Microsoft Sentinel**.
3. Selecione **law-sentinel**.
4. No painel de navegação esquerdo, expanda **Gerenciamento de ameaças** e selecione **Pastas de trabalho**.
5. Selecione **Adicionar pasta de trabalho**.
6. Selecione **Editar**.
7. Selecione o primeiro botão **Editar** no lado direito.
8. Selecione **Adicionar** > **Adicionar parâmetros**.
9.  Selecione **Adicionar parâmetro** e preencha as seguintes informações:
 - **Nome do parâmetro:** TimeRange
 - **Tipo de parâmetro**: Seletor de intervalo de tempo
10. Verifique as seguintes configurações:
 - **Obrigatório?**
11. Selecione **Salvar**.
12. No menu suspenso **TimeRange:** no canto inferior esquerdo, selecione **Últimos 7 dias**.
13. Selecione **Adicionar parâmetro** e preencha as seguintes informações:
 - **Nome do parâmetro:** AlertSeverity
 - **Tipo de parâmetro:** menu suspenso
14. Verifique as seguintes configurações:
 - **Obrigatório?**
 - **Permitir várias seleções**
 - **Ocultar o parâmetro no modo de leitura**
15. Em **Consulta de logs do workspace do Log Analytics**, cole:
```KQL
SecurityAlert
| summarize Count = count() by AlertSeverity
| order by Count desc, AlertSeverity asc
| project Value = AlertSeverity, Label = strcat(AlertSeverity, ' - ', Count)
```
16.  No menu suspenso **Intervalo de tempo**, selecione **TimeRange**.
17. Role para baixo até **Incluir no menu suspenso**, marque **Todos** e defina o **Item selecionado padrão** como **Todos**.
18. Selecione **Salvar**.
19. Selecione **Adicionar parâmetro** e preencha as seguintes informações:
 - **Nome do parâmetro:** ProductName
 - **Tipo de parâmetro:** menu suspenso
20. Verifique as seguintes configurações:
 - **Obrigatório?**
 - **Permitir várias seleções**
 - **Ocultar o parâmetro no modo de leitura**
21. Em **Consulta de logs do workspace do Log Analytics**, cole:
```KQL
SecurityAlert
| summarize Count = count() by ProductName
| order by Count desc, ProductName asc
| project Value = ProductName, Label = strcat(ProductName, ' - ', Count)
```
22.  No menu suspenso **Intervalo de tempo**, selecione **TimeRange**
23. Role para baixo até **Incluir no menu suspenso**, marque **Todos** e defina o **Item selecionado padrão** como **Todos**.
24. Selecione **Salvar**.
25. Selecione **Adicionar** e **Adicionar consulta**.
26. Em **Consulta de logs do workspace do Log Analytics**, cole:
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
27. Escolha **TimeRange** no menu suspenso Intervalo de Tempo.
Você configurará o conteúdo dinâmico para obter todos os alertas para o incidente selecionado. Os alertas serão exportados e estarão disponíveis fora dessa consulta. 
28.  Selecione a guia **Configurações avançadas** na parte superior da janela **Edição de consulta**.
29. Verifique as seguintes configurações:
- **Quando os itens estiverem selecionados, exportar os parâmetros** 
30.  Selecione **Adicionar Parâmetro** e preencha as seguintes informações:
   - **Campo a ser exportado:** Alertas
   - **Nome do parâmetro:** Alertas
31.  Selecione **Salvar**. 
32. Retorne à guia **Configurações**.
33. Selecione **Executar Consulta**.
34. Selecione **Configurações de Coluna**.
35. Selecione **IncidentUrl**.
36. Defina o renderizador de coluna como **Link**.
37. Em Configurações de link, defina **Exibir para abrir** como **URL**.
38. Selecione **Salvar e Fechar**.

Você criará a exibição de alertas com base em qual incidente está selecionado. 

39. Selecione **+ Adicionar** na parte inferior da janela **Edição do item de consulta**. Selecione **Adicionar consulta**.
40. Cole o KQL na Consulta de logs do workspace do Log Analytics 
```KQL
SecurityAlert
| where SystemAlertId in ({Alerts})
| summarize by  DisplayName, StartTime, EndTime,  SystemAlertId
| sort by EndTime desc
```
41. Escolha **TimeRange** no menu suspenso Intervalo de tempo.
42. Selecione **Done Editing**.
43. Selecione **Edição concluída** na barra superior da janela **Nova pasta de trabalho**.
44. Selecione um **Incidente**.
45. Alertas para o incidente vinculado aparecerão abaixo.

Você criou um painel com exibições personalizadas para incidentes e os alertas associados.
