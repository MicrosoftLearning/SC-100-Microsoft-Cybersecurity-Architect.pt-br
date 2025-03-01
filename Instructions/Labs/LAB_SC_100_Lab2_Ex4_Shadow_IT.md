---
lab: 3
title: Exercício 4 - Shadow IT
---


# Laboratório 2 - Exercício 4 - Shadow-IT

A infraestrutura de TI da Contoso evoluiu nas últimas décadas, fornecendo várias instâncias de servidor, aplicativos e serviços. Recentemente, a empresa priorizou a proteção de seu ambiente implementando gerenciamento de dispositivos, governança de dados e proteção de identidade e aplicativos nos últimos dois anos. No entanto, o processo de restringir os usuários apenas a aplicativos específicos implantados pela empresa ainda não foi estabelecido, permitindo que os usuários instalem aplicativos de várias fontes. Como arquiteto de segurança cibernética da organização, seu objetivo é ter uma visão geral completa de todos os aplicativos usados pelos funcionários. Sua medida de proteção é bloquear aplicativos inseguros em seu ambiente. 

## Parte 1: Criar uma solução (obrigatório)

Nesta tarefa, você criará um conceito para resolver os desafios que a Contoso Ltd. está enfrentando.

### Abordagem de design

No cenário especificado, sua ação inicial é analisar e descobrir todos os aplicativos atualmente em uso pelos funcionários. Aplicativos não autorizados instalados pelos usuários podem representar riscos de segurança para a empresa, destacando a necessidade de se identificar a Shadow IT. A etapa seguinte é remediar os riscos apresentados por esses aplicativos inseguros.

Defender para Aplicativos de Nuvem é uma solução de segurança projetada para lidar com os riscos de Shadow IT em ambientes de nuvem. Ela ajuda as organizações a descobrir e monitorar aplicativos em nuvem não autorizados utilizados pelos funcionários, avaliar sua postura de segurança e aplicar políticas que garantam a conformidade e protejam os dados. Ao oferecer visibilidade e controle sobre a Shadow IT, Defender para Aplicativos de Nuvem ajuda as organizações a reduzir os riscos de segurança associados ao uso não autorizado da nuvem, aprimorando a segurança de seu ambiente de nuvem.

### Solução Proposta

|Requisito|Solução|Plano de ação|
|----|----|----|
|Descubra a Shadow IT|Microsoft Defender para Aplicativos de Nuvem|Investigue todos os aplicativos no ambiente da Contoso|
|Bloqueie todos os aplicativos não seguros|Microsoft Defender para Aplicativos de Nuvem|Marque os aplicativos não seguros como não sancionados|

## Parte 2: Implementar a solução (opcional)

### Tarefa 1: Integrar o Microsoft Defender para Ponto de Extremidade com o Defender para Aplicativos de Nuvem 

Para se controlar o uso do aplicativo em dispositivos de propriedade da empresa de usuários, você deve integrar o Defender para Ponto de Extremidade ao Defender para Aplicativos de Nuvem.

1. Entre no portal do **https://security.microsoft.com/** Microsoft Defender como Allan Deyoung usando sua conta de administrador **Administrador MOD**.
2. No portal do Microsoft Defender, expanda **Busca** e selecione **Busca Avançada**. Aguarde a conclusão da preparação dos novos espaços.
3. No portal do Microsoft Defender, no menu de navegação à esquerda, selecione **Configurações**.
4. Na página **Configurações**, selecione **Pontos de Extremidade**.
5. Na página **Pontos de Extremidade**, em **Geral**, selecione **Recursos avançados**.
6. Habilite o **Microsoft Defender para Aplicativos de Nuvem**.
7. Selecione **Salvar preferências** na parte inferior.

Você habilitou com êxito Microsoft Defender para Aplicativos de Nuvem para Pontos de Extremidade. Com essa configuração, todos os sinais provenientes do Microsoft Defender para Pontos de Extremidade são enviados para o Defender para Aplicativos de Nuvem, dando a você a capacidade de bloquear aplicativos não seguros. Todos os aplicativos marcados como **não sancionados** agora serão bloqueados.

### Tarefa 2: Investigar a Shadow-IT da Contoso Ltd.

Nesta tarefa, você analisará todos os aplicativos usados atualmente em sua empresa. Você examinará mais de perto vários aplicativos e suas respectivas avaliações de risco, bem como sua estrutura de avaliação.

1. Você deve estar no portal do Microsoft Defender **https://security.microsoft.com/**.
2. No portal do Microsoft Defender, na página de navegação à esquerda, expanda **Aplicativos de nuvem** e selecione **Cloud Discovery**.
3. Na página **Cloud Discovery, **selecione **Aplicativos descobertos**.
4. A folha **Aplicativos descobertos** exibe todos os aplicativos atualmente utilizados em sua organização. Explore vários aplicativos e suas pontuações de risco associadas selecionando cada aplicativo respectivo.

> [!NOTE] O Defender para Aplicativos de Nuvem classifica os riscos com base em certificações regulatórias, padrões do setor e práticas recomendadas. A pontuação reflete a maturidade da adequação do aplicativo para uso corporativo. Ele calcula uma pontuação total para cada aplicativo calculando a média das subpontuações ponderadas em várias categorias de risco que incluem considerações de confiabilidade.

Você examinou com êxito vários aplicativos que são usados atualmente na Contoso.

### Tarefa 3: Bloquear aplicativos não seguros

Depois de obter uma visão geral do uso de aplicativos em seu ambiente, sua primeira ação de correção é bloquear aplicativos não seguros.

1. Você deve estar no portal do Microsoft Defender **https://security.microsoft.com/**.
2. No portal do Microsoft Defender, na página de navegação à esquerda, expanda **Aplicativos de nuvem** e selecione **Cloud Discovery**.
3. Na página **Cloud Discovery, **selecione **Aplicativos descobertos**.
4. Defina o filtro para **Pontuação de risco** como 0 - 4.
5. Selecione **Selecionar em massa** e, depois, **Tudo**.
6. Selecione os três pontos e acesse **Mais ações**.
7. Selecione **Marcar como não sancionado**.
8. Selecione **Salvar**.
   
Você bloqueou com sucesso o uso de aplicativos vulneráveis pelos usuários.

### Tarefa 4: Bloquear aplicativos não seguros automaticamente

Para bloquear automaticamente aplicativos não seguros no futuro, você criará uma política de descoberta de aplicativos personalizada. Essa política marcará aplicativos não seguros como **Não sancionados**. Como você integrou o Defender para Ponto de Extremidade ao Defender para Aplicativos de Nuvem, esses aplicativos serão bloqueados automaticamente.

1. Você deve estar no portal do Microsoft Defender **https://security.microsoft.com/**.
2. No portal do Microsoft Defender, na página de navegação à esquerda, expanda **Aplicativos de nuvem** e selecione **Cloud Discovery**.
3. Na página **Aplicativos descobertos**, selecione **+ Nova política baseada na pesquisa**.
4. Insira as seguintes informações:
    - **Nome da política**: Marque os aplicativos não seguros como não sancionados
    - **Gravidade da política**: Média
    - **Descrição para usuários**: os aplicativos com pontuação de risco 4 ou menos não serão sancionados e bloqueados automaticamente.
5. Em **Aplicativos que correspondem a todos os itens a seguir**, adicione um filtro e defina-o como **Pontuação de risco igual a 0-4**.
6. Em **Alertas**, selecione **Criar um alerta para cada evento correspondente com a gravidade da política** e defina o valor de **Limite de alerta diário por política** como 5.
7. Em **Ações de governança**, selecione **Marcar aplicativo como não sancionado**.
8. Selecione **Criar**.

Você criou uma política para marcar aplicativos com pontuação de risco 5 ou inferior como não sancionados.