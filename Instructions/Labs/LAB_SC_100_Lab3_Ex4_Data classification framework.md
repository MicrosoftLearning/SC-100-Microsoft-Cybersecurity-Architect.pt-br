---
lab: 3
title: Exercício 4 — Estrutura de classificação de dados
---


# Laboratório 3 — Exercício 4 — Estrutura de classificação de dados

Você recebeu a tarefa de estruturar a classificação de dados para a Contoso Ltd. em preparação para uma auditoria ISO-27001:2022. O objetivo é estabelecer uma estrutura robusta que seja crucial para garantir uma proteção eficaz dos dados contra vazamento, exclusão e perdas. Sua função envolve a integração de um novo sistema de identificação de projetos para projetos de construção dentro da empresa. Para cumprir os regulamentos governamentais, todos os documentos que contêm um determinado ID de projeto devem ser mantidos por 5 anos.

Você recebeu os seguintes exemplos para classificar IDs de projeto:

|ID do projeto|
|----|
|PAR-1023-DA
|BER-0822-AB
|Rom-0419-bm
|sTr*1223-Se
|BaR#0418-ag|
|dui0522-in|

## Parte 1: Criar uma solução (obrigatório)

Nesta tarefa, você criará um conceito para resolver os problemas que a Contoso Ltd. está enfrentando.

### Abordagem de design

Essa introdução de uma nova ID de projeto requer a criação de um tipo de informação confidencial (SIT) correspondente, que requer o desenvolvimento de um padrão personalizado que incorpore uma expressão regular. Posteriormente, esse SIT pode ser usado para se criar um rótulo de retenção e uma política de rotulagem automática associada.

### Solução Proposta

|Requisito|Solução|Plano de ação|
|----|----|----|
|Identificar documentos que contenham IDs de projeto|Proteção de Informações do Microsoft Purview|Criar um tipo de informação confidencial personalizada|
|Cumprir a regulamentação governamental de reter dados por 5 anos| Gerenciamento do Ciclo de Vida de Dados do Microsoft Purview|Implementar uma política de retenção|

## Parte 2: Implementar a solução (opcional)

### Tarefa 1: Criar um tipo de informações confidenciais personalizado

Você criará um tipo de informação confidencial personalizado para detectar documentos que contenham IDs de projeto.

1. Entre no portal de Conformidade do Microsoft Purview **https://compliance.microsoft.com/** como Allan Deyoung usando sua conta **Administrador do MOD**.
1. No portal de conformidade do Microsoft Purview, expanda **Classificação de dados** e, em seguida, escolha **Classificadores**.
3. Na página **Classificadores**, selecione **Tipos de informações confidenciais** > **Criar tipo de informações confidenciais**.
4. Na página **Nomear seu tipo de informações confidenciais**, insira as seguintes informações:
    - **Nome**: Número de identificação do projeto
    - **Descrição**: Identifica o número de identificação do projeto
1. Selecione **Avançar**.
1. Na página **Definir padrões para este tipo de informação confidencial**, selecione **Criar padrão**.
1. Na página **Novo padrão**, selecione **Adicionar elemento primário** e, em seguida, **Expressão regular**.
1. Na página **Adicionar uma expressão regular** na caixa de texto **ID**, digite **ProjectID**.
1. Na caixa de texto **Expressão regular**, insira a expressão a seguir:
```regex   
[a-zA-Z]{3}(\W)?[\d]{4}(\W)?[a-zA-Z]{2}
```
> [!NOTE] A expressão regular fornecida é elaborada de forma a identificar uma sequência caracterizada por três letras possivelmente seguidas por caracteres não-palavra, depois por quatro dígitos, também possivelmente seguidos por caracteres não-palavra e, finalmente, terminando com duas letras. A presença de caracteres não-palavra é discricionária, e o padrão abrangente destina-se a corresponder a um formato ou estrutura específica dentro dos dados.

1. Selecione **Correspondência de cadeia de caracteres** para as **expressões regulares** e selecione **Concluído**.
1. Selecione **Alta confiança** para **Nível de confiança** na parte superior e selecione **Criar**.
1. Conclua a configuração e crie o tipo de informação confidencial.

Você criou com êxito um novo tipo de informação confidencial para identificar IDs de projeto.

### Tarefa 2: Criar um rótulo de retenção

Você criará um rótulo de retenção para reter todos os documentos relacionados a projetos de construção por cinco anos.

1. Você deve estar registrado na página inicial do portal de conformidade do Microsoft Purview**https://compliance.microsoft.com/**.
1. No portal de conformidade do Microsoft Purview, no painel de navegação esquerdo, expanda **Gerenciamento do ciclo de vida dos dados** e selecione **Microsoft 365**.
1. Na página **Gerenciamento do ciclo de vida dos dados**, selecione a folha **Rótulos**.
1. Na folha **Rótulos**, selecione **Novo rótulo**.
1. Na página **Nomer política de retenção**, insira as seguintes informações:

    - **Nome**: Retenção da documentação do projeto de construção
    - **Descrição para os usuários**: A Política de Retenção de Documentação do Projeto de Construção determina a retenção de todos os documentos relacionados ao projeto por cinco anos após a conclusão do projeto
    - **Descrição para administradores**: Este rótulo é aplicado para reter documentos do projeto de construção por um período de cinco anos e é utilizado em conjunto com a rotulagem automática.

1. Selecione **Avançar**
1. Na página **Definir configurações de rótulo**, escolha **Reter itens para sempre ou por um período específico** e clique em **Avançar**.
1. Na página **Definir o período de retenção**, insira as seguintes informações:

    - **Manter os itens por**: 5 anos
    - **Iniciar o período de retenção com base em**: quando os itens foram criados
    - **Ao final do período de retenção**: não fazer nada

1. Selecione **Avançar**.
1. Na página **Escolher o que acontece após o período de retenção**, selecione **Desativar configurações de retenção**.
1. Conclua a configuração e crie o rótulo de retenção sem publicá-lo.

Você criou um rótulo de retenção com um período de retenção de cinco anos.

### Tarefa 3: Publicar automaticamente o rótulo de retenção

Você usará o tipo de informação confidencial criado neste exercício para aplicar automaticamente o rótulo de retenção.

1. Você deve estar registrado na página inicial do portal de conformidade do Microsoft Purview**https://compliance.microsoft.com/**.
1. No portal de conformidade do Microsoft Purview, expanda **Gerenciamento do Ciclo de Vida dos Dados** e selecione **Microsoft 365**..
1. No painel Gerenciamento do ciclo de** vida dos **dados, selecione **a folha Rotular políticas**.
1. Na folha **Políticas de rótulo**, selecione **Aplicar um rótulo automaticamente**.
1. Na página **Introdução**, insira as seguintes informações:

    - **Nome**: Rotular documentos relacionados a projetos de construção
    - **Descrição**: esta política aplica automaticamente a política "Retenção da documentação de projeto de construção" em qualquer documento referente a projetos de construção.

1. Selecione **Avançar**.
1. Na página **Escolher o tipo de conteúdo ao qual você deseja aplicar este rótulo**, selecione **Aplicar rótulo ao conteúdo que contém informações confidenciais** e selecione **Avançar**.
1. Na página **Conteúdo que contém informações confidenciais**, selecione **Personalizado**, **Política personalizada** e **Avançar**.
Na página **Definir conteúdo que contém informações confidenciais**, adicione o tipo de informação confidencial personalizado que você criou **Número de Identificação do Projeto**. Depois, especifique as seguintes configurações:

    - **Nome do grupo**: pesquisa de ID do projeto
    - **Nível de confiança**: Alta confiança
    - **Contagem de instâncias**: 1 para qualquer

1. Selecione **Avançar**
1. Na página **Escopo da política**, selecione **Avançar**.
1. Na página **Escolher o tipo de política de retenção para criar**, selecione **Estática** e clique em **Avançar**.
1. Aplique o rótulo a todos os locais disponíveis.
1. Na página **Escolha um rótulo para aplicar automaticamente**, selecione **Adicionar rótulo** e, em seguida, selecione o rótulo **Retenção da documentação do projeto de construção** que você criou na tarefa 2 e selecione **Adicionar**.
1. Ative e conclua a configuração para criar a política de rotulagem automática.

Você publicou e aplicou automaticamente o rótulo de retenção a todos os documentos que contêm as IDs do projeto.