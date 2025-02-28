# Sincronização entre locatários

A Contoso adquiriu recentemente a Tailwind Traders e tem sido difícil determinar quais convidados são clientes ou parceiros e quais são funcionários da empresa adquirida. Sua tarefa é elaborar uma lista de endereços comuns inicial da Tailwind Traders para a Contoso. Além disso, seu locatário deve permitir que apenas nomes de domínio conhecidos sejam adicionados como usuários convidados ao Entra ID. Você deseja limitar quem pode convidar convidados para a organização apenas para usuários internos. Você restringirá o acesso externo a apenas um domínio. Você também criará uma colaboração B2B e uma sincronização entre locatários da Tailwind Traders para a Contoso.

Como arquiteto de segurança cibernética, você deve garantir que todos os requisitos sejam atendidos e implementar as alterações necessárias no Entra ID para aplicar os princípios de Confiança Zero. Neste exercício, você criará, junto com um parceiro de laboratório, uma sincronização entre locatários.

## Parte 1: Criar uma solução (obrigatório)

Nesta tarefa, você criará um conceito para atender aos requisitos que a Contoso Ltd. e a Tailwind Traders estão enfrentando.

### Abordagem de design

A etapa inicial envolve análise dos requisitos com base no cenário descrito, entendendo-se os objetivos e a definição dos requisitos.

Com base no caso de uso em questão, os seguintes requisitos podem ser descritos:

- Sincronizar os usuários de ambas as empresas
- Tornar os usuários externos identificáveis como externos
- Restringir os direitos de convite apenas a funcionários internos 
- Restringir o acesso externo a domínios confiáveis da empresa

Na segunda etapa, examine o ambiente atual da Contoso Ltd. O Microsoft Entra ID oferece soluções que permitem a colaboração externa. Investigue quais controles existem e quais políticas já estão em vigor. Use o portal do Entra ID para revisar as configurações e políticas atuais e determinar quais ajustes devem ser implementados para atender aos requisitos necessários.

A terceira fase envolve a elaboração do conceito da solução. Após a investigação, fica evidente que a sincronização entre locatários é a melhor maneira de permitir que a colaboração atenda a todos os requisitos.  

### Solução proposta

|Requisito|Solução|Plano de ação|
|----|----|----|
|Restringir os direitos de convite apenas a funcionários internos|Configurações da colaboração externa|Limitar os direitos de convite a membros do locatário e funções de convite de administrador específicas|
|Bloquear convites de todos, exceto da lista de domínios confiáveis|Configurações da colaboração externa|Criar uma lista de permissões de convite, incluindo apenas domínios confiáveis|
|Sincronizar os usuários de ambas as empresas|Sincronização entre locatários do Entra ID|Estabeleça confiança de acesso entre os dois locatários do Entra ID e crie uma configuração que sincronize os usuários com o outro locatário|
|Tornar os usuários externos identificáveis como externos|Mapeamento de atributos entre locatários|Editar o atributo displayName de cada usuário sincronizado criando uma expressão personalizada usando a função de mapeamento de atributo da configuração de sincronização entre locatários|

## Parte 2: Implementar a solução (opcional)

### Tarefa 1 - Formação da equipe e preparativos

Nesta tarefa, você verificará os pré-requisitos de uma sincronização entre locatários e se juntará a um parceiro de laboratório.

1. Faça logon na VM do Cliente 1 (LON-Sc1) como a conta **lon-sc1\admin** . A senha deve ser fornecida pelo seu provedor de hospedagem de laboratório.
1. Abra o **Microsoft Edge**, selecione a barra de endereços, navegue até **`https://entra.microsoft.com`** e entre no Portal do Entra ID como **Administrador do MOD**admin@WWLxZZZZZZ.onmicrosoft.com (em que ZZZZZZ é sua ID de locatário exclusiva fornecida pelo seu provedor de hospedagem do laboratório). A senha de administrador deve ser fornecida pelo seu provedor de hospedagem do laboratório.
1. Se você for solicitado a configurar a autenticação multifator, siga as instruções.
1. Na caixa de diálogo **Permanecer conectado?** selecione a caixa de seleção **Não mostrar novamente** e, em seguida, selecione **Não**.
1. Feche a caixa de diálogo de salvamento de senha selecionando **Agora não**, para não salvar as credenciais do administrador global padrão em seu navegador.
1. No painel de navegação esquerdo, navegue até **Visão geral** > **Identidade**.
1. Anote a **ID do locatário** e o **Domínio primário** apresentados na guia **Visão geral**.
1. Troque sua **ID de locatário** e **Domínio primário** com seu parceiro de laboratório.

Você deve ter um plano de qual topologia deseja usar, quais usuários estarão no escopo do primeiro teste de sincronização e como deseja mapeá-los para o locatário do Entra ID da Contoso.

### Tarefa 2 – Configurar o acesso entre locatários

Como agora você preparou as informações necessárias para a implementação da sincronização entre locatários, agora executará as etapas necessárias para que seu locatário acesse o locatário de seus parceiros e vice-versa.

1. Você ainda deve estar registrado no portal Entra ID **https://entra.microsoft.com**.
1. No painel de navegação à esquerda, navegue até **Identidade** > **Identidades Externas** > **Configurações de acesso entre locatários**.
1. Selecione a guia **Configurações da organização** e **Adicionar organização**.
1. Preencha o campo **ID do locatário ou nome de domínio** com a ID do locatário fornecida pelo parceiro de laboratório e selecione **Adicionar**.
1. Em **Acesso de entrada** para a Contoso, selecione **Herdado do padrão** para acessar as configurações de sincronização entre locatários para esse locatário específico.
1. Nas **Configurações de confiança**, habilite **Resgatar convites automaticamente com o locatário da Contoso**.
1. Selecione **Salvar**.
1. Em **Sincronização entre locatários**, habilite **Permitir que os usuários sincronizem com este locatário**.
1. Selecione **Salvar** e feche a caixa de diálogo usando o **X** no canto superior direito.
1. Em **Acesso de saída** para a Contoso, selecione **Herdado do padrão** para acessar as configurações de sincronização entre locatários para esse locatário específico.
1. Em **Configurações de confiança**, habilite **Resgatar convites automaticamente com o locatário da Contoso**.
1. Selecione **Salvar** e feche a caixa de diálogo usando o **X** no canto superior direito.

Você habilitou seu locatário para sincronizar nos dois sentidos com o locatário do seu parceiro sem a necessidade de os usuários resgatarem os convites manualmente. 

### Tarefa 3 – Restringir o acesso externo

Nesta tarefa, você restringirá a capacidade de convidar novos usuários convidados para sua organização, controlando o escopo de usuários com permissão para enviar convites. Você limitará o escopo dos domínios que podem ser convidados como convidados para o domínio de locatário do seu parceiro.

1. Você ainda deve estar registrado no portal Entra ID **https://entra.microsoft.com**.
1. No painel de navegação esquerdo, navegue até **Identidades** > **Identidades Externas** > **Configurações de colaboração externa**.
1. Na seção **Configurações de convite de convidado**, selecione **Os usuários membros e os usuários atribuídos a funções de administrador específicas podem convidar usuários convidados, incluindo os convidados com permissões de membro**.
1. Em **Restrições de colaboração**, selecione **Permitir convites somente para os domínios especificados**.
1. Adicione o domínio do parceiro de laboratório **WWLxZZZZZZ.onmicrosoft.com** (em que ZZZZZZ é a ID de locatário exclusiva do parceiro de laboratório fornecida pelo provedor de hospedagem do laboratório).
1. Selecione **Salvar**.

Agora você restringiu quem pode convidar e quem pode receber convite para seu locatário.

### Tarefa 4 – Criar uma configuração

Nesta tarefa, você criará uma configuração básica e testará a conexão com o outro locatário.

1. Você ainda deve estar registrado no portal Entra ID **https://entra.microsoft.com**.
1. No painel de navegação esquerdo, navegue até **Identidade** > **Identidades externas** > **Sincronização entre locatários** > **Configurações**.
1. Criar uma **Nova configuração**.
1. Insira o nome **Sincronização entre locatários da Contoso** e selecione **Criar**.
1. Em **Provisionamento**, altere o **Modo de provisionamento** para **Automático**.
1. Na caixa **ID do locatário**, insira a ID do locatário do parceiro que você anotou na Tarefa 1.
1. Selecione **Testar Conexão**.
1. Selecione **Salvar**.

Você configurou as configurações de acesso corretamente e verá uma mensagem informando que as credenciais fornecidas estão autorizadas a habilitar o provisionamento. Se a conexão de teste falhar, verifique se seu parceiro inseriu o domínio correto na Tarefa 3 e configurou a sincronização entre locatários, conforme descrito na Tarefa 2.

### Tarefa 5 – Definir o escopo do usuário

Nesta tarefa, você definirá quem está no escopo da primeira sincronização.

1. Você ainda deve estar no portal do Entra ID **https://entra.microsoft.com** nas configurações de provisionamento da configuração recém-criada. Caso contrário, siga estas três etapas para voltar:
   1. No painel de navegação esquerdo, navegue até **Identidade** > **Identidades externas** > **Sincronização entre locatários** > **Configurações**.
   1. Selecione **sincronização entre locatários da Contoso**
   1. Navegue até **Provisionamento**.
1. Expanda a seção **Configurações**.
1. Verifique se o menu suspenso Escopo está definido como **Sincronizar somente usuários e grupos atribuídos**.
1. Se precisou alterar esta configuração, selecione **Salvar**.
1. Selecione **Usuários e grupos** no painel de navegação.
1. Selecione **Adicionar usuário/grupo**.
1. Na página **Adicionar atribuição**, selecione **Nenhum selecionado**.
1. Pesquise **Jurídico** e destaque a **Equipe Jurídica** usando a caixa de seleção e clique em **Selecionar**.
1. Selecione **Atribuir** para adicionar a equipe composta por dois usuários ao escopo de sincronização.

Agora você definiu seu primeiro escopo de usuários para sincronização com o locatário do seu parceiro.

### Tarefa 6 — Revisar mapeamentos de atributo

Nesta tarefa, você revisará os mapeamentos de atributo e garantirá que os usuários sincronizados apareçam na lista de endereços global da Contoso.

1. Você ainda deve estar no portal do Entra ID **https://entra.microsoft.com** nas configurações **Usuários e grupos** da configuração de sincronização entre locatários. Caso contrário, siga estas duas etapas para voltar à página de configuração:
   1. No painel de navegação esquerdo, navegue até **Identidade** > **Identidades externas** > **Sincronização entre locatários** > **Configurações**.
   1. Selecione **Sincronização entre locatários da Contoso**.
1. Navegue até **Provisionamento** e expanda a seção **Mapeamentos**.
1. Selecione **Provisionar usuários do Microsoft Entra ID**.
1. No atributo **showInAddressList**, selecione Editar.
1. Verifique se Tipo de mapeamento está definido como **Constante** e se o valor está definido como **verdadeiro**.
1. Selecione **OK**.
1. No atributo **displayName**, selecione **Editar**.
1. Altere o Tipo de mapeamento para **Expressão**.
1. Remova a expressão preexistente.
1. Selecione **Usar o Construtor de Expressões**.
1. Selecione a função **Acrescentar**.
1. No campo **Selecionar atributo**, selecione o atributo **[displayName]** na lista suspensa.
1. No campo **Inserir sufixo**, insira **" (Contoso)"** incluindo o espaço na frente do colchete, mas sem as aspas.
1. Selecione **Adicionar expressão**. A expressão à direita será assim: `Append([displayName], " (Contoso)")`
1. Você pode testar sua expressão selecionando um usuário.
1. Selecione **Aplicar expressão** e selecione **Ok** para sair da caixa de diálogo de edição.
1. Selecione **Salvar**.
1. Feche a página Mapeamento de atributos clicando no **X** no canto superior direito da página.

Agora você se certificou de que todos os usuários sincronizados aparecerão na lista de endereços global do outro locatário. Você também adicionou uma expressão (Contoso) ao nome de exibição de cada usuário sincronizado no outro locatário.

### Tarefa 7 — Habilitar o provisionamento e testar com seu parceiro de laboratório

Nesta tarefa, você habilitará o provisionamento e testará se os usuários aparecem no outro locatário da maneira que você precisa. Como o provisionamento automático pode levar algum tempo, acionaremos um provisionamento manual.

1. Você ainda deve estar no portal do Entra ID **https://entra.microsoft.com** nas configurações Provisionamento da configuração de sincronização entre locatários. Caso contrário, siga estas duas etapas para voltar à página de configuração:
   1. No painel de navegação esquerdo, navegue até **Identidade** > **Identidades externas** > **Sincronização entre locatários** > **Configurações**.
   1. Selecione **sincronização entre locatários da Contoso**
1. Navegue até **Provisionar sob demanda**.
1. Pesquise **`Grady Archie`** como membro da **Equipe jurídica** com escopo.
1. Selecione **Provisionar**.
    - Você receberá uma confirmação assim que o provisionamento for concluído.
1. Feche a página de ação Executar clicando no **X** no canto superior direito da tela.

Você acabou de provisionar seu primeiro usuário manualmente e, ao verificar a lista de usuários do locatário do parceiro, verá o usuário Grady Archie (Contoso).

### Tarefa 8 – Distribuir a sincronização completa

Como o primeiro provisionamento de usuário foi testado com êxito, agora você provisionará o restante da lista de usuários para o outro locatário.

1. Você ainda deve estar no portal do Entra ID **https://entra.microsoft.com** na página **Provisionar sob demanda** de sua configuração de sincronização entre locatários. Caso contrário, siga estas duas etapas para voltar à página de configuração:
   1. No painel de navegação esquerdo, navegue até **Identidade** > **Identidades externas** > **Sincronização entre locatários** > **Configurações**.
   1. Selecione **sincronização entre locatários da Contoso**
1. Selecione **Usuários e grupos**.
1. Selecione **Adicionar usuário/grupo**.
1. Na página **Adicionar atribuição**, selecione **Nenhum selecionado**.
1. Selecione o grupo **Todos os funcionários**, pois esse é o grupo que contém **todos os funcionários da Contoso**.
1. Confirme a seleção.
1. Selecione **Atribuir**.

Agora você criou uma sincronização entre locatários entre seu locatário e outro locatário. Você conseguirá adaptar tudo o que fez em seu locatário de demonstração no sistema produtivo da Tailwind Traders e ajudá-los a se integrar à Contoso.
