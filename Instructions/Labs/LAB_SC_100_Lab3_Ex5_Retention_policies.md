---
lab: 3
title: Exercício 5 — Políticas de retenção
---

# Laboratório 3 — Exercício 5 — Políticas de retenção

O governo alemão modificou recentemente leis específicas que regem os períodos de retenção para empresas. Uma mudança significativa é que todos os documentos financeiros agora devem ser retidos por 11 anos em vez do requisito anterior, de 10 anos. Outra mudança é que a correspondência comercial ou empresarial, incluindo cópias de correspondência comercial ou empresarial despachada, agora pode ser retida por 5 anos em vez de 7. Atualmente, sua empresa cumpre uma política de retenção que retém todos os documentos por um período de 7 anos. No entanto, a Contoso Ltd. encontrou desafios nos últimos anos devido ao acúmulo de um grande volume de dados em seu ambiente. Isso levou ao aumento dos custos de manutenção e ao consumo significativo de espaço de armazenamento. Sua tarefa é otimizar a política de retenção da sua empresa para que se cumpram os regulamentos legais e, ao mesmo tempo, minimizem-se os requisitos de armazenamento de dados. A política da empresa determina que todos os dados devem ser retidos por pelo menos cinco anos após a criação, em estrita conformidade com todas as leis aplicáveis que regem a retenção de dados.

## Parte 1: Criar uma solução (obrigatório)

Nesta tarefa, você criará um conceito para resolver os desafios que a Contoso Ltd. está enfrentando.

### Abordagem de design

A etapa inicial envolve a análise dos requisitos com base no problema descrito e a compreensão dos objetivos

Com base no caso de uso em questão, os seguintes requisitos podem ser descritos:

- Reter todos os dados financeiros por 11 anos
- Reter toda a correspondência comercial por 5 anos
- Minimização da sobrecarga de armazenamento de dados

Na segunda etapa, examine o ambiente atual da Contoso Ltd. A Contoso tem várias soluções prontas para reter seus dados por um tempo específico. Sua tarefa é analisar a configuração atual e decidir se eles cumprem os requisitos legais. 

A terceira fase envolve a elaboração do conceito da solução. Após uma investigação minuciosa, fica claro que nenhuma das políticas existentes preenche os critérios especificados. Portanto, um novo conjunto de políticas é essencial.

Com base no cenário acima, o Gerenciamento do Ciclo de Vida de Dados do Microsoft Purview pode ser usado para reter os dados adequadamente.

### Solução Proposta

|Requisito|Solução|Plano de ação|
|----|----|----|
|Reter todos os dados financeiros por 11 anos| Gerenciamento do Ciclo de Vida de Dados do Microsoft Purview|Criar e aplicar automaticamente um rótulo de retenção.|
|Reter toda a correspondência comercial por 5 anos| Gerenciamento do Ciclo de Vida de Dados do Microsoft Purview|Implementar uma política de retenção|


## Parte 2: Implementar a solução (opcional)

### Tarefa 1: Analisar a estrutura atual da política de retenção

Nesta tarefa, você se familiarizará com a política de retenção existente da sua empresa. Você verá diferentes políticas de retenção, rótulos e políticas de rótulos. Você usará o módulo do PowerShell de Segurança e Conformidade e verá as políticas existentes. Você investigará a configuração atual e decidirá se as políticas de retenção existentes são suficientes para que a Contoso Ltd. cumpra os requisitos legais. 

>[!NOTE] Você já deve ter instalado o módulo Exchange Online PowerShell. Se o módulo não estiver disponível, siga as instruções para instalá-lo.

1. Abra uma janela com privilégios elevados do PowerShell, clicando no botão Windows com o botão direito do mouse e selecionando **Windows PowerShell (Admin)**.
1. Confirme a janela **Controle de Conta de Usuário** com **Sim**.
1. Execute o seguinte cmdlet para instalar a versão mais recente do módulo PowerShell do Exchange Online:

    ```powershell
    Install-Module ExchangeOnlineManagement
    ```
1. Confirme a caixa de diálogo de segurança do repositório não confiável com **Y** para Sim e pressione **Enter**.  Esse processo pode levar algum tempo para ser concluído.
1. Insira o seguinte cmdlet para se conectar ao PowerShell de Segurança e Conformidade:

    ```powershell
    Connect-IPPSSession
    ```
1. Insira o seguinte cmdlet para ver as políticas e configurações de retenção existentes:

    ```powershell
     Get-ComplianceTag | Format-Table -Auto Name,Priority,RetentionAction,RetentionDuration,Workload
    ```
1. Reserve algum tempo para avaliar a tabela resultante.

>[!NOTE] Você também pode acessar o portal de Conformidade do Microsoft Purview para ver políticas de retenção, mas precisa examinar cada política uma a uma em vez de obter uma visão geral de todas as suas políticas rapidamente.

Você visualizou com êxito os rótulos e configurações existentes para decidir se eles cumprem os requisitos legais.

### Tarefa2: Criar uma política de retenção.

Você cumpriu a avaliação das políticas de retenção da Contoso Ltd. e descobriu uma configuração desatualizada que não cumpre os padrões legais. Sua investigação revelou cinco políticas de retenção que compartilham configurações idênticas, com apenas um rótulo de retenção aplicado, nenhuma das quais cumpre adequadamente os requisitos legais.

Seu plano envolve a implementação de uma nova política de retenção em toda a empresa, com um período de retenção de cinco anos. Após esse período, os dados podem ser retidos, mas sua exclusão não é obrigatória. Esse ajuste cumpre os requisitos legais de períodos mínimos de retenção e reduz a sobrecarga de dados.

1. Entre no portal de Conformidade do Microsoft Purview **https://compliance.microsoft.com/** como Allan Deyoung usando sua conta **Administrador do MOD**.
1. Selecione **Gerenciamento do ciclo de vida dos dados** >  **Microsoft 365.**
1. Na página **Gerenciamento do ciclo de vida dos dados**, selecione a guia **Políticas de retenção** e selecione **+ Nova política de retenção**.
1. Na página **Nome da sua política de retenção**, insira as seguintes informações:
    - **Nome**: política geral de retenção
    - **Descrição**: Esta política é a política de retenção padrão para toda a organização. Todos os dados devem ser retidos por pelo menos 5 anos. 
1. Selecione **Avançar**.
1. Na página **Escopo da política**, clique em **Avançar**.
1. Na página **Escolher o tipo de política de retenção a ser criada**, selecione **Estática** e clique em **Avançar**.
1. Na página **Escolher onde aplicar esta política**, habilite os seguintes locais:

    - Caixas de correio do Exchange
    - Sites clássico e de comunicação do SharePoint
    - Contas do OneDrive
    - Caixas de correio do Grupo do Microsoft 365 e sites

1. Selecione**Avançar**.
1. Na página **Decidir se deseja reter o conteúdo, excluí-lo ou ambos**, insira as seguintes configurações:

    - **Reter itens por um período específico**: 5 anos
    - **Iniciar o período de retenção com base em**: quando os itens foram criados
    - **Ao final do período de retenção**: não fazer nada

1. Selecione **Avançar**.
1. Na página **Examinar e concluir**, selecione **Enviar**.

Você concluiu a criação de uma política de retenção. Agora você pode excluir todas as políticas de retenção restantes, pois elas não atendem aos requisitos da empresa.

### Tarefa3: Criar um rótulo de retenção

Para cumprir os regulamentos alemães, você criará um rótulo de retenção com um período de retenção de 11 anos e o aplicará automaticamente a todos os documentos que contenham dados financeiros alemães.

1. Você deve estar registrado na página inicial do portal de conformidade do Microsoft Purview**https://compliance.microsoft.com/**.
1. No portal de Conformidade do Microsoft Purview, na página de navegação à esquerda, expanda **Gerenciamento do ciclo de vida dos dados** e selecione **Microsoft 365**.
1. Na página **Gerenciamento do ciclo de vida dos dados**, selecione a guia **Rótulos** e selecione **+ Criar um rótulo**.
1. Na página **Nomeie sua política de retenção**, insira as seguintes informações:

    - **Nome**: Dados financeiros alemães
    - **Descrição para usuários**: Este rótulo retém todos os dados financeiros alemães por 11 anos
    - **Descrição para administradores**: O rótulo retém todos os dados financeiros por 11 anos e é aplicado automaticamente.

1. Selecione **Avançar**.
1. Na página **Definir configurações de rótulo**, selecione **Impor ações após um período específico** e selecione **Avançar**.
1. Na página **Definir o período**, insira as seguintes informações:

    - **Quanto tempo dura o período?**: 11 anos
    - **Quando o período deve começar?**: quando os itens foram criados

1. Selecione **Avançar**.
1. Na página **Escolher o que acontece após o período**, selecione **Excluir itens automaticamente**.
1. Na página **Revisar e concluir**, selecione **Criar rótulo**.
1. Na página **Seu rótulo de retenção foi criado**, selecione **Aplicar automaticamente este rótulo a um tipo específico de conteúdo** e selecione **Concluído**.
1. Na página **Vamos iniciar** , insira as seguintes informações:

    - **Nome**: Reter automaticamente todos os dados financeiros alemães por 11 anos
    - **Descrições**: esta política aplica automaticamente o rótulo **Dados financeiros alemães**.

1. Selecione **Avançar**.
1. Na página **Escolher o tipo de conteúdo ao qual você deseja aplicar este rótulo**, selecione **Aplicar rótulo ao conteúdo que contém informações confidenciais** e selecione **Avançar**.
1. Na página **Conteúdo que contém informações confidenciais**, defina o filtro como **Alemanha** e selecione **Financeiro** e, em seguida, **Dados financeiros da Alemanha** e, em seguida, selecione **Avançar**.
1. Na página **Definir conteúdo que contém informações confidenciais**, selecione **Avançar**.
1. Na página **Escopo da política**, selecione **Avançar**.
1. Na página **Escolher o tipo de política de retenção a ser criada**, selecione **Estática**.
1. Na **página Escolha onde aplicar automaticamente o rótulo**, habilite os seguintes locais:

    - Caixas de correio do Exchange
    - Sites clássicos e de comunicação do SharePoint
    - Contas do OneDrive
    - Caixas de correio do Grupo do Microsoft 365 e sites

1. Selecione **Avançar**.
1. Na página **Escolher um rótulo para aplicar automaticamente**, clique em **Avançar**.
1. Em **Decidir se deseja testar ou executar a política**, selecione **Ativar política** e selecione **Avançar**.
1. Na página **Examinar e concluir**, selecione **Enviar**.

Você publicou e aplicou automaticamente um rótulo de retenção.
