# Estrutura de classificação de dados

Você recebeu a tarefa de estruturar a classificação de dados para a Contoso Ltd. em preparação para uma auditoria ISO-27001:2022. O objetivo é estabelecer uma estrutura robusta que seja crucial para garantir uma proteção eficaz dos dados contra vazamento, exclusão e perdas. Sua função envolve a integração de um novo sistema de identificação de projetos para projetos de construção dentro da empresa. Para cumprir os regulamentos governamentais, todos os documentos que contêm um determinado ID de projeto devem ser mantidos por 5 anos.

Você recebeu os seguintes exemplos para classificar IDs de projeto:

|ID do projeto|
|----|
|PAR-1023-DA|
|BER-0822-AB|
|Rom-0419-bm|
|sTr*1223-Se|
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

1. Entre no portal de Conformidade do Microsoft Purview**`https://purview.microsoft.com/`** como Allan Deyoung usando sua conta de **Administrador MOD**.
1. Se você for solicitado a configurar a autenticação multifator, siga as instruções.
1. Você é levado para a nova página de aterrissagem do portal do Microsoft Purview. Selecione a caixa ao lado da frase “**Eu concordo com os termos de divulgação de fluxo de dados e políticas de privacidade**”, e depois selecione **Começar**.
1. No painel de navegação à esquerda, selecione **Soluções** e **Proteção de informações**. Como alternativa, na janela principal, você pode selecionar o bloco **Exibir todas as soluções** e, em seguida, selecionar o bloco **Proteção de Informações** listado em Segurança de Dados.
1. Expanda **Classificadores** e escolha **Tipos de informações confidenciais**.
1. Na página **Tipos de informações confidenciais**, selecione **Criar tipo de informações confidenciais**.
1. Na página **Nomear seu tipo de informações confidenciais**, insira as seguintes informações:
    - Nome: **`Project Identification Number`**
    - Descrição: **`Identifies project identification number`**
1. Selecione **Avançar**.
1. Na página **Definir padrões para este tipo de informação confidencial**, selecione**Criar padrão**.
1. Na página **Novo padrão**, selecione **Adicionar elemento primário** e, em seguida, **Expressão regular**.
1. Na página **Adicionar uma expressão regular**, na caixa de texto **ID**, digite **`ProjectID`**.
1. Na caixa de texto **Expressão regular**, insira a seguinte expressão:

    **`[a-zA-Z]{3}(\W)?[\d]{4}(\W)?[a-zA-Z]{2}`**

    >[!NOTE] A expressão regular fornecida é elaborada de forma a identificar uma sequência caracterizada por três letras possivelmente seguidas por caracteres não-palavra, depois por quatro dígitos, também possivelmente seguidos por caracteres não-palavra e, finalmente, terminando com duas letras. A presença de caracteres não-palavra é discricionária, e o padrão abrangente destina-se a corresponder a um formato ou estrutura específica dentro dos dados.

1. Na caixa de texto Expressão regular, selecione **Correspondência de cadeia de caracteres** e selecione **Concluído**.
1. Na janela **Novo padrão**, em **Nível de confiança**, selecione **Alta confiança**, **Criar** e **Avançar**.
1. Na página **Escolher o nível de confiança recomendado para mostrar nas políticas de conformidade**, deixe a configuração como **Alto nível de confiança** e selecione **Avançar**.
1. Em **Revisar configurações e concluir**, verifique as configurações, selecione **Criar** e, quando a política for criada, selecione **Concluído**.

Você criou com êxito um novo tipo de informação confidencial para identificar IDs de projeto.

### Tarefa 2: Criar um rótulo de retenção

Você criará um rótulo de retenção para reter todos os documentos relacionados a projetos de construção por cinco anos.

1. Você ainda deve estar no portal do Microsoft Purview **https://purview.microsoft.com/**.
1. No painel de navegação esquerdo, selecione **Soluções** e, em seguida, **Gerenciamento do Ciclo de Vida de Dados**.
1. Selecione **Rótulos de retenção**.
1. Na página **Rótulos**, selecione **Criar um rótulo**.
1. Na página **Nomear rótulo de retenção**, insira as seguintes informações:

    - Nome: **`Retention of Construction Project Documentation`**
    - Descrição para usuários: **`The construction project documentation Retention Policy dictates the retention of all project-related documents for five years following project completion.`**
    - Descrição para administradores: **`This label is applied to retain construction project documents for a period of five years, and it is utilized in conjunction with auto-labeling.`**

1. Selecione **Avançar**
1. Na página **Definir configurações de rótulo**, escolha **Reter itens para sempre ou por um período específico** e clique em **Avançar**.
1. Na página **Definir o período de retenção**, insira as seguintes informações:

    - Reter os itens por: **5 anos**
    - Iniciar o período de retenção com base em: **quando os itens foram criados**

1. Selecione **Avançar**.
1. Na página **Escolher o que acontece após o período de retenção**, selecione **Desativar configurações de retenção** e clique em **Avançar**.
1. Na página **Revisar e concluir**, revise as configurações e selecione **Criar rótulo**.
1. Na página **Seu rótulo de retenção foi criado**, você tem várias opções.  Selecione **Não fazer nada** e **Concluído**.  Você criará a política de aplicação automática na próxima tarefa. Selecionar Aplicar este rótulo automaticamente a um tipo específico de conteúdo orientará você pelas etapas da tarefa subsequente, começando na etapa 4.

1. Mantenha a guia do navegador aberta para a próxima tarefa.

Você criou um rótulo de retenção com um período de retenção de cinco anos.

### Tarefa 3: Publicar automaticamente o rótulo de retenção

Você usará o tipo de informação confidencial criado neste exercício para aplicar automaticamente o rótulo de retenção.

1. Você ainda deve estar na solução de Gerenciamento do Ciclo de Vida dos Dados no portal do Microsoft Purview.  Caso contrário, navegue até **`https://purview.microsoft.com/`** > **Soluções** > **Gerenciamento do ciclo de vida de dados**.
1. No painel **Gerenciamento do Ciclo de Vida dos Dados**, selecione **Políticas de rótulo**.
1. Na folha **Políticas de rótulo**, selecione **Aplicar um rótulo automaticamente**.
1. Na página **Introdução**, insira as seguintes informações:

    - Nome: **`Label documents related to construction projects`**
    - Descrição: **`This policy automatically enforces the "Construction Project Documentation Retention" policy on any document pertaining to construction projects.`**

1. Selecione **Avançar**.
1. Na página **Escolher o tipo de conteúdo ao qual você deseja aplicar este rótulo**, selecione **Aplicar rótulo ao conteúdo que contém informações confidenciais** e selecione **Avançar**.
1. Na página **Conteúdo que contém informações confidenciais**, selecione **Personalizado**, **Política personalizada** e **Avançar**.

1. Em **Definir conteúdo que contém informações confidenciais**, especifique as seguintes configurações:
    - Nome do grupo: **`Project ID lookup`**
    - Em Tipos de informações confidenciais, selecione **Adicionar** e **Tipos de informações confidenciais**.  
    - Na página Tipos de informações confidenciais, no campo de pesquisa, digite o nome do rótulo que você criou **`Project Identification number`** e pressione Enter.  Selecione **Número de identificação do projeto** e **Adicionar**.
    - Deixe o Nível de confiança como **Alta confiança**.
    - Deixe a contagem de instâncias como **1 para Qualquer**.
    - Selecione **Avançar**
1. Na página **Escopo da política**, deixe a configuração Unidades de Administração como **Diretório completo** e selecione **Avançar**.
1. Na página **Escolher o tipo de política de retenção para criar**, selecione **Estática** e clique em **Avançar**.
1. Na página **Escolher onde aplicar automaticamente o rótulo**, verifique se o status está definido como **Ativado** para todos os locais disponíveis e selecione **Avançar**.
1. Na página **Escolher um rótulo para aplicar automaticamente**, selecione **Adicionar rótulo** e selecione o rótulo **Retenção da documentação do projeto de construção** que você criou na tarefa anterior, selecione **Adicionar** e **Avançar**.
1. Na página **Decidir se deseja testar ou executar a política**, selecione **Ativar política** e selecione **Avançar**.
1. Na página **Revisar e concluir**, revise as suas configurações, selecione **Enviar** e **Concluído**.

Você publicou e aplicou automaticamente o rótulo de retenção a todos os documentos que contêm as IDs do projeto.
