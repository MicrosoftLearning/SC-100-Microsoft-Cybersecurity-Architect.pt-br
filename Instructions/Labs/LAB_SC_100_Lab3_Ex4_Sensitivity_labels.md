---
lab: 3
title: Exercício 4 — Rótulos de confidencialidade
---

# Laboratório 3 – Exercício 4 – Rótulos de confidencialidade

A Contoso Ltd. está em processo de aquisição da Tailwind Traders. A gerência decidiu tratar todos os documentos neste processo como estritamente confidenciais para minimizar o risco de vazamento de dados.

Você recebeu os seguintes requisitos de segurança para o rótulo:

- O conteúdo só pode ser compartilhado com funcionários internos da Contoso Ltd.
- O conteúdo deve ser criptografado.
- Arquivos e emails não podem ser encaminhados.
- O acesso ao conteúdo de dispositivos não corporativos é proibido.
- O escopo deste rótulo é a gerência.

## Parte 1: Criar uma solução (obrigatório)

Nesta tarefa, você criará um conceito para resolver os problemas que a Contoso Ltd. está enfrentando.

### Abordagem de design

A Contoso tem várias soluções para proteger dados. A sua abordagem inicial será analisar a configuração atual e decidir se a empresa atende aos requisitos atuais. 

Com base no cenário acima, a Proteção de Informações do Microsoft Purview pode ser usada para atender aos requisitos e proteger os dados adequadamente. Os rótulos de confidencialidade da Proteção de Informações do Microsoft Purview permitem que você classifique e proteja os dados da sua organização, garantindo que a produtividade do usuário e os recursos colaborativos permaneçam desimpedidos. 

### Solução Proposta

|Requisito|Solução|Plano de ação|
|----|----|----|
|Criptografar documentos e emails|Proteção de Informações do Microsoft Purview|Implantar um rótulo de confidencialidade|
|Restringir o acesso a dados de dispositivos não gerenciados|Proteção de Informações do Microsoft Purview|Implantar um rótulo de confidencialidade|
|Restringir o acesso apenas a usuários internos|Proteção de Informações do Microsoft Purview|Implantar um rótulo de confidencialidade

## Parte 2: Implementar a solução (opcional)

### Tarefa 1: Investigar rótulos de confidencialidade existentes

Nesta tarefa, você investigará os rótulos de confidencialidade existentes e decidirá se um novo rótulo precisa ser criado.

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
1. Quando a janela **Entrar** for exibida, entre como `admin@WWLxZZZZZZ.onmicrosoft.com` (em que ZZZZZZ é sua ID de locatário exclusiva fornecida pelo provedor de hospedagem de laboratório) e use a senha administrativa do seu locatário.
1. Insira o cmdlet a seguir para obter uma lista de todos os rótulos de confidencialidade de implantações

    ```powershell
    Get-Label | Format-Table -wrap ParentLabelDisplay,DisplayName,LabelActions
    ```
Esse cmdlet mostra todos os rótulos de confidencialidade implantados e as ações correspondentes. Examine os rótulos. Decida se os rótulos existentes atendem aos requisitos de negócios ou se uma nova rotulagem é necessária. Quando terminar, continue com a próxima tarefa.

### Tarefa 2: Habilitar o suporte a rótulo de confidencialidade para grupos e sites

Em uma tarefa anterior, você revisou os rótulos existentes e chegou à conclusão de que os rótulos existentes atuais não atendem aos requisitos de negócios da empresa. Para aplicar rótulos de confidencialidade a grupos e sites, você precisa habilitar o suporte a rótulos de confidencialidade no PowerShell.

1. Abra uma janela privilégios elevados do PowerShell clicando no menu Iniciar com o botão direito do mouse e selecionando Windows PowerShell e execute-o como administrador.
1. Confirme a janela Controle de Conta de Usuário com Sim e pressione Enter.
1. Primeiro, precisamos instalar o SDK do PowerShell do Microsoft Graph. Como ele vem em dois módulos, Microsoft.Graph e Microsoft.Graph.Beta, precisamos instalar ambos. Insira o seguinte cmdlet para instalar o Microsoft.Graph mais recente:

```powershell
Install-Module Microsoft.Graph -Scope CurrentUser
```
1. Confirme a caixa de diálogo de segurança do Nuget e a caixa de diálogo Segurança do repositório não confiável com S para Sim e pressione Enter. Esse processo pode levar algum tempo para ser concluído.
1. Insira o seguinte cmdlet para instalar o Microsoft.Graph.Beta:

```powershell
Install-Module Microsoft.Graph.Beta -Scope CurrentUser
```
1. Confirme a janela Controle de Conta de Usuário com Sim e pressione Enter.
1. Conecte-se ao locatário:

```powershell
Connect-MgGraph -Scopes "Directory.ReadWrite.All"
```

1. No formulário Entrar na sua conta, entre como admin@WWLxZZZZZZ.onmicrosoft.com, (em que zzzzzz é a sua ID de locatário exclusiva fornecida pelo seu provedor de hospedagem de laboratório). A senha deve ser fornecida pelo seu provedor de hospedagem de laboratório.
1. Na janela de **permissões solicitadas**, selecione **Consentir em nome de sua organização** e selecione **Aceitar**. Depois de entrar, selecione a janela do PowerShell.
1. Insira o seguinte cmdlet para habilitar rótulos de confidencialidade:

```powershell
$params = @{
     Values = @(
        @{
            Name = "EnableMIPLabels"
            Value = "True"
        }
     )
}

Update-MgBetaDirectorySetting -DirectorySettingId $grpUnifiedSetting.Id -BodyParameter $params
```

1. Feche a janela do PowerShell.

Você habilitou o suporte para rótulos de confidencialidade para grupos e sites.

### Tarefa 3: Criar e implantar um rótulo de confidencialidade de alta segurança

Você criará um novo rótulo de confidencialidade para atender aos requisitos.

1. Entre no portal de Conformidade do Microsoft Purview **https://compliance.microsoft.com/** como Allan Deyoung usando sua conta **Administrador do MOD**.
1. No portal do Microsoft Purview, no painel de navegação à esquerda, expanda **Proteção de Informações** e selecione **Rótulos**.
1. Na página **Rótulos**, selecione **+ Criar um rótulo**.
1. Na página **Fornecer detalhes básicos desse rótulo**, insira as seguintes informações:

    - **Nome**: Confidencial — Processo de aquisição
    - **Nome de exibição**: Confidencial — Processo de aquisição
    - **Descrição para usuários**: Dados altamente confidenciais relacionados a qualquer processo de aquisição.
    - **Descrição para administradores**: este rótulo fornece proteção a todos os dados relacionados a qualquer aquisição da Contoso.

1. Selecione **Avançar**.
1. Na página **Definir o escopo deste rótulo**, selecione **Itens**, depois selecione **Arquivos**, **Emails** e **Grupos e sites**. Se alguma outra opção nesta página estiver selecionada, desmarque-a.
1. Na página **Escolher configurações de proteção para os itens rotulados**, clique em **Aplicar ou remover criptografia**.
1. Na página **Criptografia**, selecione **Definir configurações de criptografia**.
1. Nas configurações de criptografia, insira as seguintes informações: 
    - **Atribuir permissões agora ou permitir que os usuários decidam?**: permitir que os usuários atribuam permissões ao aplicar o rótulo.
    - **No Outlook, imponha uma das seguintes restrições**: Não encaminhar.
1. Selecione **No Word, PowerPoint e Excel, solicite que os usuários especifiquem permissões** e selecione **Avançar**.
1. Na página **Rotulagem automática para arquivos e emails**, clique em **Avançar**.
1. Na página **Definir configurações de proteção para grupos e sites**, selecione **Privacidade e acesso de usuário externo** e **Compartilhamento externo e Acesso condicional** e selecione **Avançar**.
1. Na página **Configurações de privacidade de dados e acesso de usuário externo**, selecione **Privado** e **Avançar**.
1. Na página **Definir configurações de compartilhamento externo e acesso condicional**, selecione **Controlar o compartilhamento externo de sites rotulados do SharePoint** e **Usar o Acesso condicional do Microsoft Entra para proteger sites rotulados do SharePoint** e defina a configuração da seguinte maneira:
    - **O conteúdo pode ser compartilhado com**: Apenas pessoas da organização.
    - **Determinar se os usuários podem acessar sites do SharePoint em dispositivos não gerenciados**: Bloquear acesso
1. Selecione **Avançar**.
1. Na página **Rotulagem automática para ativos de dados esquematizados (versão prévia),** clique em **Avançar**.
1. Na página **Revisar configurações e concluir**, selecione **Criar rótulo**.
1. Na página **Seu rótulo de confidencialidade foi criado**, como próxima etapa, clique em **Publicar rótulo nos aplicativos dos usuários**.
1. Selecione **Concluído**.
1. No painel **Publicar rótulo**, clique em **Criar nova política de rótulo**.
1. Na página **Escolher rótulo de confidencialidade para publicar**, selecione o rótulo que você acabou de criar e selecione **Avançar**.
1. Na página **Atribuir unidades de administração**, clique em **Avançar**.
1. Na página **Publicar para usuários e grupos**, selecione **Usuários e grupos** e **Editar**.
1. Na página **Escopo para usuários e grupos**, selecione **Usuários e grupos específicos** e selecione **+ Incluir usuários e grupos**, selecione **Executivos** e **Liderança** e selecione **Concluído** até que a atribuição de usuário seja concluída.
1. Selecione **Avançar**.
1. Na página **Configurações de política**, selecione **Os usuários devem fornecer uma justificativa para remover um rótulo ou diminuir sua classificação** e **Exigir que os usuários apliquem um rótulo aos emails e documentos**.
1. Selecione **Avançar**.
1. Na página **Configurações padrão para documentos**, selecione **O email herda o rótulo de prioridade mais alta dos anexos** e selecione **Avançar**.
1. Na página **Configurações padrão para reuniões e eventos do calendário**, clique em **Avançar**.
1. Na página **Configurações padrão para grupos e sites**, clique em **Avançar**.
1. Na página **Configurações padrão para conteúdo do Fabric e do Power BI**, clique em **Avançar**.
1. Na página **Nomer política**, insira as seguintes informações:
    - **Nome**: Política de rótulo de confidencialidade de gerenciamento
    - **Descrição**: Esta política destina-se à gerência para proteger em relação à aquisição de empresas
1. Selecione **Avançar**.
1. Na página **Examinar e concluir**, selecione **Enviar**.

Você criou e publicou um rótulo de confidencialidade.