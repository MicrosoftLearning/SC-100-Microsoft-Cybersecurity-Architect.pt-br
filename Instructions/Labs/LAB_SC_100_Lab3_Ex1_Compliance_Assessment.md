---
lab: 3
title: Exercício 1 — Avaliação de conformidade
---

# Laboratório 3 — Exercício 1 — Avaliação de conformidade

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

1. Entre no portal de Conformidade do Microsoft Purview **https://compliance.microsoft.com/** como Allan Deyoung usando sua conta **Administrador do MOD**.
2. Você será solicitado a configurar a autenticação multifator, siga as instruções.
3. À esquerda no painel de navegação do portal de conformidade do Microsoft Purview, selecione **Gerenciador de Conformidade**.
4. Na página **Gerenciador de Conformidade**, selecione **Avaliação**.
5. Na página **Gerenciador de Conformidade \| Avaliações**, selecione **+ Adicionar avaliação**.
6. Na página **Basear sua avaliação em um regulamento**, selecione **Selecionar regulamento**.
7. Na caixa de texto de pesquisa, insira **ISO-27001:2022**, selecione o regulamento, selecione **Salvar** e **Avançar**.
8. Na página **Adicionar nome e grupo**, na caixa de texto **Nome da avaliação**, insira **Avaliação de auditoria do ISO-27001** e selecione **Avançar**.
9. Na página **Selecionar serviços**, selecione **Selecionar serviços**, **Microsoft 365** e selecione **Adicionar** e **Avançar**
10. Conclua a configuração e crie a avaliação.

Você criou uma avaliação com base na ISO-27001.

### Tarefa 2: Atribuir tarefas a um engenheiro técnico

Os resultados da avaliação mostram diferentes áreas e ações que são essenciais para cumprir os regulamentos da ISO-27011. Você investigará ações de melhoria e atribuirá uma tarefa a um engenheiro técnico.

1. Você deve estar registrado na página inicial do portal de conformidade do Microsoft Purview**https://compliance.microsoft.com/**.
2. À esquerda no painel de navegação do portal de conformidade do Microsoft Purview, selecione **Gerenciador de Conformidade**.
3. Na página **Gerenciador de Conformidade**, selecione a avaliação **ISO/IEC-27001:2022** que você criou.
4. Na página de avaliação, selecione a folha **Suas ações de melhoria**.
5. Defina o filtro de **Família de controle** como **Controles físicos**.
6. Selecione todas as ações de melhoria mostradas e, em seguida, selecione **Atribuir ao usuário**.
7. Na nova página **Atribuir ações de melhoria**, na caixa de texto de pesquisa, insira **Nestor Wilke**.
8. Selecione o usuário e, em seguida, **Atribuir**.

Você visualizou e atribuiu uma ação de melhoria a um engenheiro técnico

### Tarefa 3: Fornecer acesso a um engenheiro técnico para as ações de melhoria.

Os usuários precisam de acesso para visualizar as tarefas atribuídas a eles. Você concederá a Nestor Wilke acesso à avaliação.

1. Você deve estar registrado na página inicial do portal de conformidade do Microsoft Purview**https://compliance.microsoft.com/**.
2. À esquerda no painel de navegação do portal de conformidade do Microsoft Purview, selecione **Gerenciador de Conformidade**.
3. Na página **Gerenciador de Conformidade**, selecione o painel **Avaliação** e, em seguida, selecione a **Avaliação de auditoria do ISO-27001**.
4. Na página **ISO/IEC 27001: Avaliação**, no canto superior direito, selecione **Gerenciar acesso do usuário**.
5. Na nova página **Gerenciar acesso do usuário**, selecione **Avaliador** e **Adicionar avaliadores**.
6. Na caixa de texto **Pesquisar usuários**, insira **Nestor Wilke**.
7. Selecione o usuário e clique em **Salvar**.

Você concedeu a Nestor Wilke acesso à avaliação.
