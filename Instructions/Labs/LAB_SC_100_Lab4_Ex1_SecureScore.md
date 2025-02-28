# Laboratório 4 — Exercício 1 — Gerenciamento da Postura de Segurança

A Contoso deseja melhorar sua postura de segurança usando o Microsoft Secure Score, uma ferramenta que fornece recomendações e diretrizes sobre como reduzir a superfície de ataque e proteger contra ameaças. A Contoso tem uma equipe de segurança dedicada que gerencia o painel de Classificação de Segurança e atribui ações a diferentes equipes de produto com base em suas funções e responsabilidades. Uma das equipes de produto, a equipe de projeto Mark 8, é responsável pelo gerenciamento de dispositivo móvel e precisa garantir que os dispositivos sejam bloqueados após um período de inatividade para impedir o acesso não autorizado.

## Parte 1: Criar uma solução (obrigatório)

### Abordagem de design

A etapa inicial envolve análise dos requisitos com base no cenário descrito, entendendo-se os objetivos e a definição dos requisitos.

Com base no caso de uso em questão, os seguintes requisitos podem ser descritos:

- Obtenha mais recomendações para aumentar a postura de segurança
- Conceder acesso limitado à recomendação 
- Informar a equipe responsável

O Microsoft Secure Score avalia a postura de segurança de uma organização em todas as cargas de trabalho do Microsoft 365. Ele fornece visibilidade centralizada, insights priorizados por ameaças e controles abrangentes para aprimorar a proteção contra ataques cibernéticos e otimizar a segurança cibernética.

### Solução proposta

|Requisito|Solução|Plano de ação|
|----|----|----|
|Adicionar mais recomendações para aumentar a postura de segurança | Fontes de dados adicionais | Habilitar fontes adicionais de “não carga de trabalho” |
|Conceder acesso limitado à recomendação |Permissão e funções do Defender XDR |Conceder acesso específico a Joni Shermann |
|Informar a equipe responsável |Pontuação segura |Informe a equipe do projeto Mark 8 |

### Compensações de design e soluções alternativas

## Parte 2: Implementar a solução (opcional)

### Tarefa 1 — Configurar fonte de dados adicional na Classificação de Segurança

Nesta tarefa, você habilitará fontes de dados adicionais para a Classificação de Segurança, para obter mais recomendações sobre sua superfície de ataque.

1. Faça logon na VM do Cliente 1 (LON-SC1) como a conta **lon-sc1\admin**. A senha deve ser fornecida pelo seu provedor de hospedagem de laboratório.
2. Abra o **Microsoft Edge**, selecione a barra de endereços, navegue até <https://security.microsoft.com> e entre no centro de administração do Microsoft 365 como **Administrador MOD**<admin@WWLxZZZZZZ.onmicrosoft.com> (em que ZZZZZZ é a sua ID de locatário exclusiva fornecida pelo seu provedor de hospedagem do laboratório). A senha de administrador deve ser fornecida pelo seu provedor de hospedagem do laboratório.
3. Na caixa de diálogo **Permanecer conectado?** selecione a caixa de seleção **Não mostrar novamente** e, em seguida, selecione **Não**.
4. Você será solicitado a configurar a autenticação multifator, siga as instruções.
5. Feche a caixa de diálogo de salvamento da senha na parte inferior selecionando **Nunca**, para não salvar as credenciais de administradores globais padrão em seu navegador.
6. No painel de navegação à esquerda, selecione **Configurações**.
7. Selecione **Microsoft Defender XDR**.
8. Em Geral, selecione **Permissões e funções**.
9. Talvez seja necessário aguardar alguns minutos para que o Microsoft Defender XDR seja configurado.
10. Habilite **Fontes de dados adicionais**.
11. Voltar para o painel do Secure Score

Você ativou Fontes de dados adicionais para configurar o acesso baseado em função para recomendações de produtos específicas.

### Tarefa 2 – Configurar o RBAC para Secure Score

Nesta tarefa, você garantirá que apenas pessoas selecionadas possam acessar essas informações. Você habilita o RBAC para Secure Score e o baseia no conceito de acesso com privilégios mínimos.

1. Você deve estar conectado ao portal do Microsoft Defender XDR.
2. No painel de navegação à esquerda, selecione **Configurações**.
3. Selecione **Microsoft Defender XDR**.
4. Selecione **Permissões e funções**.
5. Selecione **Ir para Funções e permissões**.
6. Selecione **Criar função personalizada**.
7. Nome da função: SecureScore Apps
8. Selecione **Avançar**.
9. Clique em **Postura de segurança**, selecione **Selecionar permissões personalizadas** e selecione **Selecionar permissões personalizadas**.
10. Escolha **Classificação de segurança (gerenciar).**
11. Escolha **Aplicar**.
12. Selecione **Avançar**.
13. Selecione **Adicionar atribuição**.
14. Nome da atribuição: SecureScore Manager
15. Atribua-a a **Joni Sherman**. 
16. Em **Fontes de dados**, **desmarque** tudo, exceto**Microsoft Secure Score - Fontes de dados adicionais**.
17. Selecione **Adicionar**.
18. Selecione **Avançar**.
19. Selecione **Enviar**.

Você implementou o RBAC para acessar as recomendações de fonte de dados adicionais para Joni Sherman na Classificação de Segurança.

### Tarefa 3 – Delegar uma ação

A equipe de projeto Mark 8 da Contoso é responsável pelo desenvolvimento adicional do gerenciamento de dispositivos móveis, portanto, você informará a equipe de projeto sobre sua recomendação de segurança.

1. Você deve estar conectado ao portal do Microsoft Defender XDR.
2. Escolha **Classificação de segurança** no painel de navegação à esquerda.
3. Na guia, selecione **Ações recomendadas**.
4. Procure e selecione **Garantir que os dispositivos sejam bloqueados após um período de inatividade para impedir o acesso não autorizado**.
5. Selecione **Compartilhar** e, no menu suspenso, selecione **Microsoft Teams**.
6. No campo **Equipe**, selecione **Equipe do Projeto Mark 8** e, no campo **Canal, **selecione **Pesquisa e Desenvolvimento do Canal**.
7. Selecione **Postar mensagem no Teams**.

Joni Sherman e sua equipe de projeto Mark 8 serão notificadas sobre a ação recomendada em seu canal de equipes.

### Tarefa 4 – Gerenciar recomendações

Como Joni Sherman, você recebeu a notificação das equipes de que uma ação específica para aumentar sua postura de segurança foi recomendada e gerenciará a ação recomendada e documentará a solução.

Nesta tarefa, você gerenciará a ação recomendada e documentará suas soluções.

1. Abra uma janela inPrivate do Microsoft Edge, navegue até <https://office.com> e entre como <JoniS@WWLxZZZZZZ.onmicrosoft.com>.
2. Abra o Teams e abra o canal **Pesquisa e Desenvolvimento** em **Equipe do projeto Mark 8**.
3. Revise a mensagem postada na ação Classificação de segurança.
4. Abra outra guia na janela inPrivate do Microsoft Edge e navegue até <https://security.microsoft.com>.
5. Escolha **Classificação de segurança** no painel de navegação à esquerda.
6. Selecione a guia **Ações recomendadas** para ver todas as ações às quais você tem acesso.
7. Procure e selecione **Garantir que os dispositivos sejam bloqueados após um período de inatividade para impedir o acesso não autorizado**.
8. Selecione **Editar status e plano de ação**.
9. Marque **Resolvido por meio de terceiros**.
10. Adicione uma observação **Atualmente protegido com o JAMF** ao campo **Plano de ação**.
11. Selecione **Salvar e Fechar**.

Você configurou cargas de trabalho adicionais para a Classificação de Segurança, atribuiu permissão com base no acesso de privilégio mínimo e gerenciou e delegou ações recomendadas à equipe de identidade da Contoso Ltd.
