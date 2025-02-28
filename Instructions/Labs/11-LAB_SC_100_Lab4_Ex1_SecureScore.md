# Gerenciamento da postura de segurança

A equipe de segurança da Contoso deseja melhorar sua postura de segurança usando o Microsoft Secure Score, ferramenta que fornece recomendações e diretrizes sobre como reduzir a superfície de ataque e proteger contra ameaças.

A equipe de segurança analisa e delega ações recomendadas pelo Secure Score aos membros da equipe estendida (embaixadores de segurança) que gerenciam o status e o plano de ação associados às ações de melhoria. A equipe de segurança também deseja controlar o acesso às informações de postura de segurança e às fontes de dados que as alimentam. Joni Shermann é uma das embaixadoras de segurança e precisa ter acesso ao gerenciamento de exposição.

Recentemente, houve relatos de que associados não convidados estavam sendo admitidos automaticamente em chamadas do Teams para as quais não foram convidados diretamente.  Devido à natureza sensível e confidencial das chamadas, a equipe de segurança deseja controlar isso.

## Parte 1: Criar uma solução (obrigatório)

### Abordagem de design

A guia Ações recomendadas lista as recomendações de segurança do Secure Score que abordam possíveis superfícies de ataque. Essas ações podem ser compartilhadas/delegadas.

As equipes de segurança precisam controlar o acesso às informações de postura de segurança da organização e às fontes de dados específicas que as alimentam. O modelo RBAC (controle de acesso baseado em função) unificado do Microsoft Defender XDR fornece uma experiência de gerenciamento de permissões inigualável com um ponto central para os administradores controlarem as permissões dos usuários em várias soluções de segurança.

Para garantir que os embaixadores de segurança tenham as permissões de função necessárias, você precisa criar uma função personalizada. Para que o portal de segurança do Microsoft Defender XDR comece a impor as permissões e atribuições configuradas em suas novas funções personalizadas ou funções importadas, você deve ativar o modelo RBAC unificado do Microsoft Defender XDR para algumas ou todas as suas cargas de trabalho.

### Solução proposta

|Requisito|Solução|Plano de ação|
|----|----|----|
|Joni Shermann gerenciará as ações e o status associados às recomendações de pontuação de segurança. |Gerenciamento de Exposição – Secure Score e RBAC unificado do Defender XDR | Crie uma função para gerenciar a postura de segurança e conceder acesso a Joni Shermann. |
|Controle o acesso às informações de postura de segurança e às fontes de dados que as alimentam. | RBAC unificado do Microsoft Defender XDR | Ative o RBAC Unificado do Microsoft Defender XDR para a função personalizada. |
|Compartilhe a ação recomendada do Secure Score |Pontuação segura | Compartilhe a ação recomendada |

## Parte 2: Implementar a solução (opcional)

### Tarefa 1 – Criar uma função personalizada para gerenciar a postura de segurança do Gerenciamento de Exposição

Nesta tarefa, você configurará a função personalizada focada na postura de segurança e, mais especificamente, no Gerenciamento de Exposição. Como parte da função personalizada, você concederá a Joni Shermann acesso à fonte de dados do Gerenciamento de Exposição.

1. Faça logon na VM do cliente Windows **LON-SC1** com a conta de **Administrador** local. A senha deve ser fornecida pelo seu provedor de hospedagem de laboratório.
1. Abra o **Microsoft Edge**, selecione a barra de endereços, navegue até **`https://security.microsoft.com`** e faça logon no **Microsoft Defender** como Administrador MOD **admin@WWLxZZZZZZ.onmicrosoft.com**(em que ZZZZZZ é sua ID de locatário exclusiva fornecida pelo seu provedor de hospedagem de laboratório). A senha de administrador deve ser fornecida pelo seu provedor de hospedagem do laboratório.
1. Na caixa de diálogo **Permanecer conectado?** selecione a caixa de seleção **Não mostrar novamente** e, em seguida, selecione **Não**.
1. Feche a caixa de diálogo de salvamento da senha na parte inferior selecionando **Nunca**, para não salvar as credenciais de administradores globais padrão em seu navegador.
1. Se você vir uma caixa de informações no canto superior direito da tela que diz **Gerenciar autenticação multifator**, feche-a selecionando o **X**.
1. No painel de navegação esquerdo, expanda **Sistema** e selecione **Permissões**.
1. Se esta for a primeira vez que você está acessando as configurações do Microsoft Defender, terá que aguardar alguns minutos enquanto o Defender prepara novos espaços para seus dados e os conecta.  Depois que isso for concluído, atualize a página de permissões até ver uma listagem que inclua Microsoft Defender XDR, Microsoft Entra ID, funções e grupos de pontos de extremidade, funções de colaboração e email e aplicativos de nuvem. Pode levar algum tempo para que tudo isso apareça.
1. Em **Microsoft Defender XDR(1),** selecione **Funções**.
1. Selecione **Criar função personalizada**.
1. No campo de nome Função, insira **`SecureScore Manager`** e então selecione **Avançar**.
1. Selecione **Postura de segurança**.
1. Na janela Postura de segurança:
    - Selecione **Selecionar permissões personalizadas**
    - Em Gerenciamento de postura, selecione **Selecionar permissões personalizadas**
    - Escolha **Gerenciamento de Exposição (gerenciar)**
    - Escolha **Aplicar**.
    - Selecione **Avançar**.
1. Na página **Atribuir usuários e fontes de dados**, selecione **Adicionar atribuição** e preencha os campos da seguinte maneira:
    - Nome da atribuição: **`ExposureManagement`**
    - Atribuir usuários e grupo: digite **`Joni Sherman`** e selecione-o.
    - Em **Fontes de dados**, selecione o menu suspenso para ver uma lista das fontes de dados disponíveis. Selecione somente **Gerenciamento de Exposição de Segurança da Microsoft**.  Se outras fontes de dados estiverem listadas, desmarque-as.
    - Selecione **Adicionar**.
    - Selecione **Avançar**.
1. Na página **Revisar e concluir**, revise as suas configurações e clique em **Enviar**.
1. Você deve estar na página **Permissões e funções** e ver a função personalizada que acabou de criar. Mantenha essa guia do navegador aberta, pois você vai usá-la na próxima tarefa.

Você configurou com êxito uma função personalizada para a postura de segurança que concede a Joni Shermann acesso à fonte de dados do Gerenciamento de Exposição.

### Tarefa 2 – Ativar o RBAC unificado do Defender XDR para cargas de trabalho específicas

Para que o portal de segurança do Microsoft Defender XDR comece a impor as permissões e atribuições configuradas em suas novas funções personalizadas, você deve ativar o modelo RBAC unificado do Microsoft Defender XDR para suas cargas de trabalho.

Quando você ativa algumas ou todas as suas cargas de trabalho para usar o novo modelo de permissão, as funções e permissões para essas cargas de trabalho são totalmente controladas pelo modelo RBAC unificado do Microsoft Defender XDR no portal do Microsoft Defender.

Nesta tarefa, você explorará a página em que as cargas de trabalho são ativadas.

1. Você ainda deve estar conectado ao portal do Microsoft Defender e estar na página **Permissões e funções**. Você deve ver a função personalizada que criou.
1. Observe as informações na faixa cinza. Algumas das funções ainda não são aplicáveis porque você não ativou todas as cargas de trabalho. Selecione **Ativar cargas de trabalho**.
1. Observe a descrição em **Ativar o controle de acesso unificado baseado em função**.  Quando você ativa algumas ou todas as suas cargas de trabalho para usar o novo modelo de permissão, as funções e permissões para essas cargas de trabalho são totalmente controladas pelo modelo RBAC unificado do Microsoft Defender XDR no portal do Microsoft Defender.
1. Para este exercício, a fonte de dados para o Gerenciamento de Exposição é habilitada por padrão, e é por isso que não há nenhuma configuração para habilitar essa carga de trabalho. Se você tivesse criado uma função personalizada que incluísse permissões para outras cargas de trabalho, tais como Office 365 ou Gerenciamento de Dispositivos e Vulnerabilidades, por exemplo, precisaria ativar essas cargas de trabalho específicas para ativar a função personalizada, como parte do RBAC unificado.

Você aprendeu onde ativar o modelo RBAC Unificado do Microsoft Defender XDR para algumas ou todas as suas cargas de trabalho.

### Tarefa 3 – Compartilhar uma ação recomendada

Compartilhe uma ação recomendada do Microsoft Secure Score. Nesta tarefa, você postará a ação em um canal do Teams. Ao publicá-la no Teams, os usuários do canal verão um aviso, mas não terão acesso à fonte de dados para editar o status ou gerenciar a ação. Somente Joni Shermann, que é membro do canal do Teams e tem permissões de função, pode acessar a ação recomendada.

1. Você deve estar conectado ao portal do Microsoft Defender XDR.
1. No painel de navegação à esquerda, expanda **Gerenciamento de exposição** e clique em **Secure Score**.
1. Selecione a guia **Ações recomendadas** .
1. Pesquise **`Only invited users should be automatically admitted to Teams meetings`** e selecione-o.
1. Selecione **Compartilhar** e, no menu suspenso, selecione **Microsoft Teams**.
1. No campo **Equipe**, selecione **Equipe do Projeto Mark 8** e, no campo **Canal, **selecione **Pesquisa e Desenvolvimento do Canal**.
1. Selecione **Postar mensagem no Teams**.

Joni Sherman e sua equipe de projeto Mark 8 serão notificadas sobre a ação recomendada no canal do Teams.

### Tarefa 4 – Gerenciar recomendações

Como Joni Sherman, você recebeu a notificação do Teams de que uma ação específica para aumentar a postura de segurança da organização foi recomendada.  Como membro estendido da equipe de segurança, você tem as permissões de função para gerenciar a ação recomendada e documentar a solução.

Nesta tarefa, você gerenciará a ação recomendada e documentará suas soluções.

1. Abra uma janela InPrivate do Microsoft Edge, navegue até **`https://office.com`** e faça logon como**JoniS@WWLxZZZZZZ.onmicrosoft.com**.
1. Se a página de destino aparecer desfocada, atualize-a.
1. Selecione o ícone do inicializador de aplicativos localizado à esquerda da faixa superior que diz Contoso Electronics e selecione **Teams**.
1. Na janela Bem-vindo ao Teams, selecione **Introdução**. Pode levar um ou dois minutos para que o Teams seja configurado. Se uma tela de código QR do Teams for Mobile aparecer, feche-a.
1. Abra o Teams. Para a **equipe de projeto Mark 8**, selecione **Ver todos os canais** e, em seguida, selecione **Pesquisa e desenvolvimento**.
1. Revise a mensagem postada na tarefa anterior.
1. Na mensagem postada, selecione o link **https://security.microsoft.com/securescore?viewid=actions&actionId=meeting_autoadmitusers_v1**.  Como você, Joni Shermann, recebeu permissão por meio da função personalizada, você pode acessar o Secure Score.  Outros membros da equipe do projeto Mark 8 podem ver a postagem, mas não têm acesso ao Secure Score.
1. Selecione **Editar status e plano de ação**.
1. Marque **Resolvido por meio de terceiros**.
1. Adicione uma observação **Atualmente protegido** ao campo **Plano de ação**.
1. Selecione **Salvar e Fechar**.
1. Feche as guias inPrivate do navegador.

Como Joni Shermann, você editou com êxito o status da ação recomendada.

### Tarefa 5 (opcional) – Adele Vance acessa a postagem do Teams

Nesta tarefa, Adele Vance acessa o canal da Equipe do Projeto Mark 8 e seleciona o link na mensagem postada.

1. Abra uma janela InPrivate do Microsoft Edge, navegue até **`https://office.com`** e entre como Adele Vance, **AdeleV@WWLxZZZZZZ.onmicrosoft.com**.
1. Se a página de destino aparecer desfocada, atualize-a.
1. Selecione o ícone do inicializador de aplicativos localizado à esquerda da faixa superior que diz Contoso Electronics e selecione **Teams**.
1. Na janela Bem-vindo ao Teams, selecione **Introdução**.
1. Abra o Teams. Para a **equipe de projeto Mark 8**, selecione **Ver todos os canais** e, em seguida, selecione **Pesquisa e desenvolvimento**.
1. Revise a mensagem postada na tarefa anterior.
1. Selecione o link na mensagem postada **https://security.microsoft.com/securescore?viewid=actions&actionId=meeting_autoadmitusers_v1**.
1. Você é levado diretamente para o Microsoft Secure Score, mas não tem permissão para acessar esses dados, pois Adele Vance não foi adicionada como membro à função personalizada que você criou.
1. Feche as guias InPrivate do navegador.

Nesta tarefa, você confirmou que os membros do Projeto Mark 8 podem ver a mensagem postada para a ação recomendada para ajudar a melhorar a postura de segurança da organização, mas somente os associados que foram adicionados à função personalizada podem acessar as informações do Secure Score.
