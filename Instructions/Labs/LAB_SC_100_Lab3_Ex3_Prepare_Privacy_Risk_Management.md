---
lab: 3
title: Exercício 3 — Preparar o gerenciamento de riscos de privacidade
---


# Laboratório 3 — Exercício 3 — Preparar o Gerenciamento de Riscos de Privacidade

Como Especialista em Arquitetura de Segurança Cibernética da empresa, a Contoso encarregou você de melhorar a postura de conformidade da empresa como parte de sua expansão na Europa. Especificamente, você trabalhará para melhorar a pontuação do Gerenciamento de risco de privacidade Priva. Para fazer isso, você usará o Gerenciador de Conformidade para identificar ações de melhoria e delegar as respectivas implementações. Isso levará a uma melhoria na pontuação de conformidade do gerenciamento de riscos de privacidade. Além disso, você adicionará uma nova política para as regiões dos EUA e da UE. 

## Parte 1: Criar uma solução (obrigatório)

Nesta tarefa, você criará um conceito para atender aos requisitos da Contoso Ltd.

### Abordagem de design

A etapa inicial envolve análise dos requisitos com base no cenário descrito, entendendo-se os objetivos e a definição dos requisitos.

Com base no caso de uso em questão, os seguintes requisitos podem ser descritos:

- Administradores e outros usuários com acesso a relatórios não devem ver os nomes dos usuários
- Os riscos de privacidade precisam ser gerenciados por uma equipe designada
- Diretrizes precisam existir para riscos de privacidade

Na segunda etapa, examine o ambiente atual da Contoso Ltd. O Microsoft Priva oferece soluções para gerenciar riscos de privacidade. Investigue quais controles existem e quais políticas já estão em vigor. Use o portal de Conformidade do Microsoft Purview para examinar as configurações atuais e determinar que ajustes devem ser implementados para atender aos requisitos da região para a qual estão expandindo.

A terceira fase envolve a elaboração do conceito da solução. Após investigação, fica evidente que a criação de políticas para monitorar riscos potenciais é a melhor maneira de atender aos requisitos.  

### Solução proposta

|Requisito|Solução|Plano de ação|
|----|----|----|
|Administradores e outros usuários com acesso a relatórios não devem ver os nomes dos usuários|Ação da melhoria de conformidade|Atribua e implemente a ação de melhoria **Anonimizar nomes de usuário para usuários em determinadas funções**|
|Os riscos de privacidade precisam ser gerenciados por uma equipe designada|Funções do Microsoft Purview|Crie um grupo de funções com permissões para processar riscos de privacidade e atribua os funcionários designados|
|Diretrizes precisam existir para riscos de privacidade|Política de Gerenciamento de Riscos de Privacidade|Crie uma política de gerenciamento de riscos de privacidade para alertar a equipe de gerenciamento de riscos de privacidade sobre riscos potenciais|

## Parte 2: Implementar a solução (opcional)

## Tarefa 1 – Examinar possíveis ações de melhoria do Gerenciador de Conformidade para o Gerenciamento de Riscos de Privacidade e atribuir a eles proprietários

Nesta tarefa, você terá uma visão geral das possíveis ações de melhoria do Gerenciamento de Riscos de Privacidade e as delegará.

1. **Entre** no **portal de Conformidade do Microsoft Azure****https://compliance.microsoft.com/**.
2. No painel esquerdo, selecione **Visão geral do Gerenciamento de riscos de privacidade**.
3. Role para baixo até o cartão **Ficar a par dos regulamentos e melhorar postura de privacidade.**
4. Clique no botão **Exibir ações de melhoria**.
5. Veja as possíveis ações de melhoria. Pense em quais ações de melhoria podem ser configuradas preliminarmente por você mesmo e quais podem ser delegadas à equipe de segurança.
6. Selecione a ação de melhoria **Permitir que administradores de operações de privacidade criem e deem suporte ao cumprimento de solicitações de direitos da entidade**.
7. Leia os detalhes da melhoria.
8. Atribua **Megan Bowen** como Proprietária da ação de melhoria usando o menu suspenso.
9. Selecione **Editar detalhes** na parte superior da página.
10. Defina o **status de implementação** como **Implementado**. Porque você atribuiu a **Megan Bowen** os grupos de funções de administrador de solicitações de direitos de entidade e administrador do gerenciamento de riscos de privacidade no último exercício.
11. Selecione **Salvar e fechar** na parte superior da página.

Você atribuiu uma ação de melhoria a um funcionário de segurança.

## Tarefa 2 – Atribuir e implementar a ação de melhoria **Anonimizar nomes de usuário para usuários em determinadas funções**

Você deve garantir que os usuários sejam anônimos em todos os componentes do Priva para a ação de melhoria.

*Pule para a etapa 5 se você ainda estiver na **visão geral das ações de melhoria***.
1. **Entre** no **portal de Conformidade do Microsoft Azure****https://compliance.microsoft.com/**.
1. Selecione **Gerenciador de Conformidade** > **Ações de melhoria**.
1. Selecione a ação de melhoria **Anonimizar nomes de usuário de usuários em determinadas funções**.
1. Atribua a si mesmo o **Administrador do MOD** como Proprietário desta ação de melhoria usando o menu suspenso.
1. Em **Detalhes**, clique no link **Iniciar agora** no final da descrição **Como implementar**.
1. Verifique se a configuração **Mostrar versões anônimas de nomes de usuário** está selecionada, caso contrário, selecione-a e clique em **Salvar**.
1. Feche a guia do navegador.
1. Selecione **Editar detalhes** na parte superior da ação de melhoria **Mostrar versões anônimas de nomes de usuário**.
1. Defina o **Status da implementação** como **Implementado** e selecione **Salvar**.
1. Selecione **Salvar e fechar** na parte superior da página.

Você atribuiu e implementou uma ação de melhoria.

## Tarefa 3 – Criar uma política de gerenciamento de riscos de privacidade

Esta última tarefa é sobre a criação da política personalizada de gerenciamento de riscos de privacidade para as regiões da UE e dos EUA.

1. Acesse o **Portal de conformidade do Microsoft Purview****https://compliance.microsoft.com/**
2. No painel esquerdo, selecione **Gerenciamento de riscos de privacidade** > **Políticas**.
3. Selecione **Criar uma política** no canto superior direito.
4. Selecione **Criar** no cartão **Personalizada** .
5. Selecione o modelo de política **Minimização de dados**.
6. Insira o nome da política:**Minimização de dados EUA e UE.**
7. Insira a descrição:**Esta política destina-se a minimizar os dados relevantes de riscos de privacidade salvos de acordo com os regulamentos dos EUA e da UE.**
8. Selecione **Avançar**.
9. Selecione **Adicionar grupos de classificação**.
10. Selecione:
    - GDPR aprimorada
    - Lei GLBA (Gramm-Leach-Bliley dos EUA) aprimorada
    - Lei de HIPAA (Seguro de Saúde) dos EUA aprimorada
    - Lei Patriótica dos EUA aprimorada
    - Dados de PII (informações de identificação pessoal) dos EUA aprimorados
    - Leis de notificação de violação do estado dos EUA aprimoradas
11. Selecione **Adicionar** e **Avançar**.
12. Selecione todos os usuários e grupos e **Avançar**.
13. Selecione todos os locais e **Avançar**.
14. Defina a configuração **O item não foi modificado nos últimos (dias)** como 120.
15. Em **Escolher frequência de notificações**, selecione **Mensalmente, a cada 1**.
16. Em **Link para o treinamento de privacidade**, insira: https://learn.microsoft.com/en-us/privacy/"
17. Selecione **Avançar**.
18. Defina **Criar alertas** como **Ativado**.
19. Defina **Alto volume de dados pessoais** como 20 instâncias.
20. Selecione **Avançar**.
21. Selecione **Avançar**.
22. Revise as configurações e selecione **Enviar**.

Você criou uma política de gerenciamento de riscos de privacidade para as leis de proteção de dados dos EUA e da UE.

Você concluiu a configuração e delegação de algumas ações de melhoria, políticas de gerenciamento de riscos de privacidade e permissões de usuário. Você pode prosseguir com o próximo exercício.
