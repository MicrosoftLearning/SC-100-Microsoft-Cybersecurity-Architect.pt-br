# Acesso Condicional

Você descobriu que os funcionários estão acessando o Microsoft 365 de locais desconhecidos apesar de suas políticas de Acesso Condicional permitirem apenas o acesso de locais e dispositivos específicos. Sua investigação revelou que esses funcionários estão acessando o Microsoft 365 enquanto viajam do escritório para casa no transporte público. Esse comportamento viola os regulamentos do setor e você deseja usar a Avaliação Contínua de Acesso para evitá-lo. Além disso, você deseja implementar o nível de autenticação preparado no exercício anterior para proteger determinados aplicativos que lidam com dados de clientes. 

## Parte 1: Criar uma solução (obrigatório)

Nesta tarefa, você criará um conceito para lidar com os riscos que a Contoso Ltd. está enfrentando.

### Abordagem de design

A etapa inicial envolve a análise dos requisitos com base no problema descrito, o entendimento dos objetivos e a definição dos requisitos.

Com base no caso de uso em questão, os seguintes requisitos podem ser descritos:

- Restringir o acesso de locais inseguros/desconhecidos
- Exigir autenticação forte para aplicativos que contêm informações confidenciais

Na segunda etapa, examine o ambiente atual da Contoso Ltd. O Microsoft Entra ID oferece soluções para gerenciar e restringir o acesso do usuário com uso de políticas de acesso condicional do Entra ID. Investigue quais controles existem e quais políticas já estão em vigor. Use o portal Entra ID para revisar as configurações e políticas atuais e determinar se ajustes são necessários ou se novas políticas precisam ser implementadas.

A terceira fase envolve a elaboração do conceito da solução. Após a investigação, é evidente que ainda não há uma rede confiável configurada e nenhuma das políticas atuais atende aos requisitos definidos. Portanto, um novo conjunto de políticas de acesso condicional é essencial. 

### Solução proposta

|Requisito|Solução|Plano de ação|
|----|----|----|
|Restringir o acesso de locais inseguros/desconhecidos|Política de acesso condicional do Entra ID|Defina as redes atuais da empresa como rede confiável e restrinja o acesso aos dispositivos dentro dessa rede|
|Exigir autenticação forte para aplicativos que contêm informações confidenciais|Política de acesso condicional do Entra ID|Crie uma nova política de acesso condicional focada em aplicativos confidenciais que exigem o nível de autenticação reforçado recém-criado que exclui métodos de autenticação inseguros, como SMS e Voz|

## Parte 2: Implementar a solução (opcional)

### Tarefa 1 – Criar rede confiável

Nesta tarefa, você criará um local nomeado usando o endereço IP externo da VM para definir uma rede confiável que pode ser usada em uma política de acesso condicional nas tarefas a seguir. Você usará esse endereço porque sua máquina está localizada na rede da sua empresa.

1. Faça logon na VM do Cliente 1 (LON-Sc1) como a conta **lon-sc1\admin** . A senha deve ser fornecida pelo seu provedor de hospedagem de laboratório.
1. Abra uma janela do **PowerShell** selecionando o menu Iniciar com o botão direito do mouse e, em seguida, selecione **Terminal**.
1. Insira o seguinte cmdlet para verificar seu endereço IP externo atual: `Invoke-RestMethod -Uri "http://ifconfig.me/ip"`
1. Anote o endereço IP retornado.
1. Abra o **Microsoft Edge**, selecione a barra de endereços, navegue para **`https://entra.microsoft.com`** e faça logon no Portal do Entra ID como **Administrador do MOD**admin@WWLxZZZZZZ.onmicrosoft.com (em que ZZZZZZ é sua ID de locatário exclusiva fornecida pelo seu provedor de hospedagem do laboratório). A senha de administrador deve ser fornecida pelo seu provedor de hospedagem do laboratório.
1. Se você for solicitado a configurar a autenticação multifator, siga as instruções.
1. Na caixa de diálogo Permanecer conectado?, selecione a caixa de seleção **Não mostrar novamente** e, em seguida, selecione **Não**.
1. Feche a caixa de diálogo de salvamento de senha selecionando **Agora não**, para não salvar as credenciais do administrador global padrão em seu navegador.
1. No painel de navegação esquerdo, navegue até **Proteção** > **Acesso condicional** > **Locais nomeados**.
1. Selecione **+ Localização de intervalos de IP**.
1. Insira o nome **Rede contoso confiável**.
1. Selecione **Marcar como local confiável**.
1. Selecione **+** para adicionar o endereço IP anotado na **Etapa 4**.
1. A entrada deve ser semelhante a ``168.245.***.***/32`` (*** pode ser diferente dependendo do seu provedor de hospedagem de laboratório).
1. Selecione **Adicionar**.
1. Selecione **Criar**.

Você definiu o local nomeado e confiável do endereço IP externo da sua empresa e pode usá-lo para restringir o acesso fora da rede da empresa.

### Tarefa 2 – Criar nova Política de Acesso Condicional com escopo limitado

Como você criou com êxito uma rede confiável, agora você a usará para criar a política de Acesso Condicional para restringir o acesso fora da rede corporativa com escopo limitado ao seu usuário pessoal para poder testar e impedir um bloqueio de conta em toda a empresa pelo Entra ID.

1. Você ainda deve estar registrado no portal Entra ID **https://entra.microsoft.com**.
2. No painel de navegação, navegue até **Políticas de** > **Acesso Condicional** > **de Proteção**.
3. Selecione **+ Nova política**.
4. Digite o nome **Bloquear acesso fora da rede confiável**.
5. Selecione **0 usuários e grupos selecionados**.
6. Na guia **Incluir**, selecione **Selecionar usuários e grupos** e marque **Usuários e grupos**.
7. Selecione **Allan Deyoung** como o único usuário de teste para a política.
8. Selecione **Nenhum recurso de destino selecionado** e,em**Incluir**, selecione **Todos os aplicativos de nuvem**.
9. Selecione **0 condições selecionadas** e, em **Locais**, selecione **Não configurado**.
10. Selecione **Sim** para configurar a condição de localização.
11. Em **Incluir**, selecione **Qualquer local**.
12. Em **Excluir**, selecione **Todos os locais confiáveis**.
13. Em **Conceder**, selecione **0 controles selecionados** e alterne de **Conceder acesso** para **Bloquear acesso** e escolha **Selecionar** na parte inferior da página.
14. Em **Sessão**, selecione **0 controles selecionados**.
15. Habilite **Personalizar avaliação de acesso contínuo** e selecione **Impor estritamente políticas de localização (versão prévia)** e escolha **Selecionar** na parte inferior para confirmar.
16. Em **Habilitar política**, selecione **Ativar** e selecione **Criar**.

Você criou e habilitou sua política de CA para restringir o acesso fora de redes confiáveis que afetam apenas sua própria conta de usuário de teste.

### Tarefa 3 – Testar a política configurada

Como você criou uma política de Acesso Condicional limitando o acesso a todos os aplicativos de nuvem da sua empresa, você deve garantir que o acesso ainda seja possível.

>[!ALERTA] Esta tarefa está significativamente abreviada para fins ilustrativos!
Em um cenário do mundo real, você faria um período de teste mais longo com um grupo maior e mais representativo, para garantir que nenhum incidente imprevisível distorça o resultado.

1. Abra uma nova janela **InPrivate** no seu navegador **Microsoft Edge** selecionando o ícone da barra de tarefas com o botão direito do mouse e selecione **Nova janela InPrivate**.
1. Selecione a barra de endereços, navegue até **`https://portal.microsoft.com`** e entre no Portal do M365 como **Allan Deyoung**alland@WWLxZZZZZZ.onmicrosoft.com (em que ZZZZZZ é sua ID de locatário exclusiva fornecida pelo provedor de hospedagem de laboratório). Insira a senha de administrador que deve ser fornecida pelo seu provedor de hospedagem do laboratório.
1. Na caixa de diálogo Permanecer conectado?, selecione a caixa de seleção **Não mostrar novamente** e, em seguida, selecione **Não**.
1. Como o logon foi bem-sucedido, você pode fechar a janela **InPrivate**.
1. Volte para a janela do navegador Edge, onde você ainda deve estar conectado ao portal Entra ID **https://entra.microsoft.com**.
1. No painel de navegação esquerdo, navegue até **Proteção** > **Acesso Condicional** > **Monitoramento** > **Logs de entrada**.
1. Selecione **Adicionar filtros** e filtre pelo **Usuário** de **Allan Deyoung**.
1. Selecione a entrada de log mais recente de **Allan Deyoung**.
1. Na guia **Acesso Condicional**, selecione **Bloquear acesso fora da Rede Confiável**.
1. Selecione a atribuição de **Usuário** e veja que ela **Corresponde** por **Atribuição direta**.
1. Selecione a atribuição **Aplicativo** e veja que ela **Corresponde** por **Todos os aplicativos incluídos**.
1. Você também deve ver que a condição de **Localização** foi **Não correspondida**, pois está dentro da rede confiável que está excluída.
Se você tentasse fazer login de uma rede com um endereço IP externo diferente, essa condição corresponderia e bloquearia a tentativa de login.
1. Feche os **detalhes da Política de Acesso Condicional** e os **Detalhes da Atividade: Entradas**.

Você testou e garantiu com êxito o acesso a todos os aplicativos de nuvem de dentro da rede da empresa. Você também verificou os logs de entrada para garantir que a política funcione conforme o esperado e use as atribuições e condições corretas para restringir o acesso aos seus aplicativos de nuvem de fora da rede da empresa.

### Tarefa 4 – Distribuição da política em toda a empresa

Após o teste bem-sucedido na tarefa anterior, agora você pode habilitar a política para toda a empresa. Para fazer isso, você editará o escopo do usuário da política existente.

>[!ALERTA] As ações implementadas nesta tarefa podem levar ao bloqueio da conta!
Certifique-se de ter pelo menos uma conta de administrador de emergência que esteja excluída dessa política em um cenário de produção, do mundo real. 

1. Você ainda deve estar registrado no portal Entra ID **https://entra.microsoft.com**.
2. No painel de navegação, navegue até **Políticas de** > **Acesso Condicional** > **de Proteção**.
3. Selecione a política **Bloquear acesso fora da Rede Confiável**.
4. Em Usuários, selecione **Usuários específicos incluídos**.
5. Selecione **Todos os usuários**.
6. No aviso exibido na parte inferior da janela, selecione **Excluir usuário atual, admin@WWLxZZZZZZ.onmicrosoft.com, desta política**.
7. Selecione **Salvar**.

Agora você configurou uma política de Acesso Condicional ativa que impede que os usuários façam login fora da rede confiável que você definiu como o endereço IP externo da empresa. Isso foi testado usando um escopo de usuário limitado para garantir que todos os aplicativos em nuvem permaneçam acessíveis. Por fim, você implementou a política de AC para todos os usuários.

Você restringiu com sucesso o acesso de fora da rede confiável.

### Tarefa 5 — Exigir MFA para Salesforce

Nesta tarefa, você cria uma política de AC para impor a força de autenticação criada no exercício anterior ao entrar no Salesforce. 

>[!IMPORTANT] Importante: Esta tarefa ignorará a fase de teste. Em um cenário do mundo real, você testaria primeiro com um escopo de usuário limitado, como visto nas tarefas anteriores, e executaria uma distribuição completa após uma fase de teste bem-sucedida.

1. Você ainda deve estar registrado no portal Entra ID **https://entra.microsoft.com**.
2. No painel de navegação, navegue até **Políticas de** > **Acesso Condicional** > **de Proteção**.
3. Selecione **+ Nova política**.
4. Insira o nome **Força de autenticação do Salesforce**.
5. Selecione **0 usuários e grupos selecionados**.
6. Na guia **Incluir**, selecione **Selecionar usuários e grupos** e marque **Usuários e grupos**.
7. Selecione **Alex Wilber** em Vendas como o único usuário de teste para a política.
8. Selecione **Nenhum recurso de destino selecionado** e, em **Incluir**, selecione **Selecionar aplicativos**.
9. Em **Selecionar**, clique em **Nenhum** e pesquise **Salesforce**.
10. Para confirmar sua escolha, clique em **Selecionar**.
11. Em **Concessão**, selecione **0 controles selecionados** e habilite **Exigir força de autenticação**.
12. Selecione sua força de autenticação personalizada da **MFA reforçada** e confirme com o botão **Selecionar**.
13. Agora defina a política como **Ativada** usando a barra de controle na parte inferior e selecione **Criar**.
14. Após uma fase de teste bem-sucedida com seu escopo de usuários limitado, selecione **Força de autenticação do Salesforce**.
15. Em Usuários, selecione **Usuários específicos incluídos**.
16. Selecione **Todos os usuários**.
17. Selecione **Salvar**.

Agora você criou uma política de AC para impor sua política de força de autenticação ao Salesforce, excluindo SMS OTP e, assim, evita ataques bem-sucedidos usando a interceptação de SMS.
