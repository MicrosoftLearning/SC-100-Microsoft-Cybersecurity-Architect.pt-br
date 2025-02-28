---
lab: 3
title: Exercício 2 - Delegar solicitações de direitos de titular
---


# Laboratório 3 – Exercício 2 – Delegar solicitações de direitos de titular

A Contoso Ltd. está se preparando para a certificação ISO-27001. Como parte dessa preparação, eles precisam implementar um processo para solicitações de direitos de titular do GDPR. A empresa usará o recurso de solicitações de direitos de titular do Microsoft Priva e integrará o novo fluxo de trabalho em seu processo de auditoria de conformidade interna. 

Como especialista em arquitetura de segurança cibernética, você delegará o tratamento de DSRs europeus e configurará permissões de leitura para a auditoria. Para garantir que os funcionários que lidam com casos de DSR também não lidem com o recurso Gerenciamento de Risco de Privacidade, você criará um grupo de funções personalizado somente exibição. Os grupos de funções internos concedem permissões demais para a auditoria. 

Você atribuirá aos funcionários escolhidos as funções necessárias para lidar com solicitações de direitos do titular ou auditoria, seguindo o princípio do privilégio mínimo. Para concluir a POC, você usará a avaliação do Microsoft Priva e garantirá que os logs de auditoria estejam ativados em seu locatário. Como a auditoria de conformidade ocorre bimestralmente, você aumentará a duração da retenção da solicitação de direitos do titular para eliminar quaisquer pontos cegos entre as auditorias. 

## Parte 1: Criar uma solução (obrigatório)

Nesta tarefa, você criará um conceito para atender aos requisitos que a Contoso Ltd. está enfrentando com sua expansão na Europa.

### Abordagem de design

A etapa inicial envolve análise dos requisitos com base no cenário descrito, entendendo-se os objetivos e a definição dos requisitos.

Com base no caso de uso em questão, os seguintes requisitos podem ser descritos:

- Permitir que seu ambiente lide com solicitações de titulares de dados
- Uma equipe designada precisa lidar com DSRs
- Os limites de retenção de DSRs precisam ser modificados para cumprir o cronograma de auditoria

Na segunda etapa, examine o ambiente atual da Contoso Ltd. O Microsoft Priva oferece soluções para gerenciar solicitações de titulares de dados. Investigue quais controles existem e quais políticas já estão em vigor. Use o portal de Conformidade do Microsoft Purview para examinar as configurações atuais e determinar que ajustes devem ser implementados para atender aos requisitos da região para a qual estão expandindo.

A terceira fase envolve a elaboração do conceito da solução. Mediante investigação, fica evidente que permitir que funcionários específicos gerenciem DSRs é a melhor maneira de atender a todos os requisitos.  

### Solução proposta

|Requisito|Solução|Plano de ação|
|----|----|----|
|Permitir que seu ambiente lide com solicitações de titulares de dados|Microsoft Purview e Centro de Administração|Atribua licenças Priva e verifique se o log de auditoria unificado está habilitado|
|Uma equipe designada precisa lidar com DSRs|Funções do Microsoft Purview|Crie um grupo de funções com permissões para lidar com DSRs e delegue os funcionários designados|
|Os limites de retenção de DSRs precisam ser modificados para cumprir o cronograma de auditoria|Gerenciamento de Risco de Privacidade do Microsoft Purview|Use uma ação de melhoria para definir um limite de retenção de 90 dias para DSRs|

## Parte 2: Implementar a solução (opcional)

## Tarefa 1 – Ativar a licença de avaliação do Microsoft Priva

Nas duas primeiras tarefas, você verificará as pré-condições necessárias para usar os recursos do Microsoft Priva. Você precisa ativar a licença de avaliação do Microsoft Priva e verificar se os logs de auditoria estão habilitados em seu locatário.

1. Faça logon na **VM** com suas credenciais de administrador.
2. Abra o **Microsoft Edge**, selecione a barra de endereços, navegue até **https://compliance.microsoft.com** e faça logon no portal de Conformidade do Microsoft Purview como **Administrador MOD**admin@WWLxZZZZZZ.onmicrosoft.com (em que ZZZZZZ é sua ID de locatário exclusiva fornecida pelo seu provedor de hospedagem de laboratório). A senha de administrador deve ser fornecida pelo seu provedor de hospedagem do laboratório.
3. Quando perguntado se você deseja permanecer conectado, selecione **Não**.
4. No painel esquerdo, selecione **Gerenciamento de Riscos de Privacidade - Visão Geral** ou **Solicitações de direitos do titular**.
5. Se a avaliação não estiver ativa, selecione **ativar avaliação** na parte superior da página.

Se a avaliação já estiver ativa em seu laboratório, você ainda precisará verificar a quantidade exata de casos de solicitações de direitos do titular contidos em sua licença no centro de administração.

6. **Entre** no **Centro de administração do Microsoft 365****https://admin.microsoft.com/**.
7. No painel esquerdo, selecione **Faturamento** e **Seus produtos**.
8. Procure a licença do **Gerenciamento de Risco de Privacidade Priva**.
9. Procure a licença do **Gerenciamento de Privacidade - solicitação de direitos do titular** e veja quantos casos estão incluídos.

Você verificou com êxito se o seu locatário M365 tem licenças Microsoft Priva ativas.

## Tarefa 2 – Verificar se os logs de auditoria estão habilitados

Para que os recursos de gerenciamento de risco de privacidade funcionem, o log de auditoria deve estar ativo em seu locatário.

1. Abra uma janela do **PowerShell** com privilégios elevados selecionando o menu Iniciar com o botão direito do mouse e, em seguida, selecione **Windows PowerShell** e **executar como administrador**.
2. Execute o seguinte cmdlet para instalar a versão mais recente do módulo Exchange Online:
    ```powershell
    Install-Module -Name ExchangeOnlineManagement
    ```
3. Confirme a caixa de diálogo de segurança do Nuget e a caixa de diálogo Segurança do repositório não confiável com S para Sim e pressione Enter. Esse processo pode levar algum tempo para ser concluído.
4. Insira o seguinte cmdlet para se conectar ao serviço Exchange Online:
    ```powershell
    Connect-ExchangeOnline
    ```
5. No formulário **Entrar na sua conta**, entre com suas credenciais de administrador.
6. Depois de se conectar com êxito à PowerShell do Exchange Online, digite:
    ```powershell
    Get-AdminAuditLogConfig | Format-List UnifiedAuditLogIngestionEnabled
    ```
7. Um valor **True** para _UnifiedAuditLogIngestionEnabled_ é retornado.
8. Se um valor **False** for retornado, habilite o Log de Auditoria com o comando:
    ```powershell
    Set-AdminAuditLogConfig -UnifiedAuditLogIngestionEnabled $true
    ```
9. Um aviso de que pode levar até 60 minutos para que a alteração entre em vigor é retornado. O Log de Auditoria agora está ativado em seu locatário. Você pode verificar novamente mais tarde com o comando mencionado anteriormente.

Você confirmou com êxito que os Logs de Auditoria estão habilitados em seu locatário.

## Tarefa 3 – Criar um grupo de funções personalizado e atribuir os funcionários designados a ele

Nesta tarefa, você criará o grupo de funções somente leitura personalizado para a auditoria de conformidade da Contoso Ltd. e atribuirá os funcionários designados.

1. Entre no **portal de Conformidade do Microsoft Azure****https://compliance.microsoft.com/**.
2. Selecione a guia **Permissões** na guia **Funções e Escopos** no painel esquerdo.
3. Selecione **Funções** em Soluções do Microsoft Purview.
4. Crie um novo grupo de funções com as seguintes configurações:
    |Configuração|Valor|
    |----|----|
    |Nome|Auditoria de conformidade interna somente para visualização|
    |Descrição|Esse grupo de funções contém todas as funções necessárias para a auditoria bimestral da postura de conformidade da Contoso Ltd.|
    |Funções|Logs de auditoria somente exibição, caso somente exibição, visualizador de gerenciamento Priva|
    |Usuários|Grady Archie|
5. Selecione **Avançar** em **Adicionar funções ao grupo de funções** e prossiga para a próxima tarefa sem fechar a caixa de diálogo.

Você criou com êxito um grupo de funções personalizado com as permissões mínimas necessárias e atribuiu os funcionários designados a ele.

## Tarefa 4 – Atribuir funcionários e você mesmo aos grupos de funções internos

Agora, você precisa atribuir as permissões restantes para gerenciamento de solicitações de direitos do titular usando os grupos de funções internos.

*(Pule para 4. se você ainda estiver no menu Funções e Escopos)*
1. **Entre** no **portal de Conformidade do Microsoft Azure****https://compliance.microsoft.com/**.
2. Selecione **Funções e Escopos** > **Permissões** no painel esquerdo.
3. Selecione **Funções** no item **Soluções do Microsoft Purview**.
4. Adicione **Irvin Sayers** ao grupo de funções **Administradores de Solicitação de Direitos do Titular**.
5. Adicione **Alex Wilber** e **Joni Sherman** ao grupo de funções **Aprovadores de Solicitação de Direitos do Titular**.
6. Adicione sua conta **Administrador MOD** e **Megan Bowen** aos grupos de funções **Administradores de Gerenciamento de Privacidade** e **Administradores de Solicitação de Direitos do Titular**.

Você atribuiu todas as permissões necessárias a todos os funcionários para lidar com solicitações de direitos do titular.

## Tarefa 5 – Configurar o limite máximo de retenção de dados para solicitações de direitos do titular

Para a auditoria de conformidade bimestral, você precisa configurar o limite de retenção para solicitações de direitos do titular nesta tarefa.

[!NOTE] Pode levar até 30 minutos para que as suas alterações de grupos de funções sejam aplicadas, e isso é necessário para que você possa ver o recurso de solicitação de direitos do titular. Se você acabou de conceder a si mesmo as permissões na tarefa 4, talvez seja necessário aguardar que as alterações entrem em vigor.

1. **Entre** no **portal de Conformidade do Microsoft Azure****https://compliance.microsoft.com/**.
2. No painel esquerdo, selecione **Gerenciador de Conformidade** e, em seguida, selecione a guia **Ações de melhoria**.
3. Na parte superior da página, selecione as **Soluções:** filtre e marque **Gerenciamento de Riscos de Privacidade Priva** e **Solicitações de Direitos do Titular Priva**.
4. Selecione **Habilitar e impor limites de retenção de dados para dados envolvidos na solicitação de direitos do titular**
5. Clique em **Atribuir ao usuário** > Pesquisar **Administrador MOD** > **Atribuir**, que atribui o administrador MOD como proprietário da ação de melhoria.
6. Leia os detalhes da melhoria.
7. Selecione **Iniciar agora** na parte inferior da descrição para inserir diretamente as configurações de solicitação de direitos do titular.
8.  Selecione a guia **Períodos de retenção de dados**.
9.  Defina o valor dos **Dados coletados e relatórios** como 90 dias e selecione **Salvar**
10. Feche a guia no Edge.
11. Selecione **Editar detalhes** na parte superior da página da ação de melhoria.
12. Defina o **status de implementação** como **Implementado**.
13. Selecione **Salvar e fechar** na parte superior da página.

Você aumentou o limite de retenção de dados de solicitação de direitos do titular e atualizou a ação de melhoria.

Você concluiu a configuração do recurso de solicitações de direitos do titular e delegou o tratamento de casos de acordo. Você pode prosseguir com o próximo exercício.
