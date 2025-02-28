# Laboratório 4 — Exercício 2 — Acesso Global Seguro

Depois de configurar o servidor de monitoramento, você precisa estabelecer uma rede segura para o servidor de arquivos usando o GSA (Acesso Global Seguro). Você quer garantir que o acesso a essas máquinas seja protegido até que esses servidores de arquivos possam ser migrados para armazenamento seguro em nuvem, especialmente se a Tailwind Traders estiver trazendo servidores locais para a infraestrutura de TI da sua empresa. Você decidiu não recriar a infraestrutura de VPN da Tailwind Traders para permitir que seus funcionários acessem os servidores. 

Para estabelecer uma rede segura, você começará criando um Proxy do Azure App e registrando o cliente no Entra ID antes de criar um conector. Depois disso, você configurará uma política de acesso e instalará o cliente GSA. Por fim, você testará a conexão GSA para garantir que tudo esteja funcionando corretamente.

## Parte 1: Criar uma solução (obrigatório)

Nesta tarefa, você protegerá o acesso remoto ao seu ambiente local.

### Abordagem de design

A etapa inicial envolve análise dos requisitos com base no cenário descrito, entendendo-se os objetivos e a definição dos requisitos.

Com base no caso de uso em questão, os seguintes requisitos podem ser descritos:

- Habilite o acesso remoto seguro para servidores locais
- Integre à infraestrutura existente
- Não use a infraestrutura obsoleta da Tailwind Traders

O Acesso Global Seguro se integra à infraestrutura de nuvem existente da Contoso Ltd. e permite que seus funcionários acessem remotamente com segurança servidores locais na infraestrutura local da Tailwind Traders. Revise o GSA e considere as diferenças em relação a outras estratégias de acesso remoto aos serviços.

### Solução proposta
<!--BITE AUSFÜLLEN-->
|Requisito|Solução|Plano de ação|
|----|----|----|
|Habilite o acesso remoto seguro para servidores locais| Acesso Global Seguro do Entra ID | Habilitar o Acesso Global Seguro  |
|Integre à infraestrutura existente | Proxy de Aplicativo | Implantar proxy de aplicativo no servidor de arquivos da Contoso |

## Parte 2: Implementar a solução (opcional)

## Tarefa 1: Ativar o Acesso Global Seguro

A primeira etapa é ativar o Acesso Global Seguro em seu locatário. Isso permitirá que você use um Proxy do Azure App para fornecer acesso seguro aos recursos locais.

1. Entre na **VM do Cliente 1** (LON-SC1) como a conta **lon-sc1\admin**. A senha deve ser fornecida pelo seu provedor de hospedagem de laboratório.
2. Abra o **Microsoft Edge**, selecione a barra de endereços, navegue para **https://entra.microsoft.com** e faça logon no Portal do Entra ID como **Administrador MOD**admin@WWLxZZZZZZ.onmicrosoft.com (em que ZZZZZZ é sua ID de locatário exclusiva fornecida pelo seu provedor de hospedagem do laboratório). A senha do usuário deve ser fornecida pelo provedor de hospedagem do laboratório.
3. Será solicitado que você configure a autenticação multifator; siga as instruções.
4. Na caixa de diálogo Permanecer conectado?, selecione a caixa de seleção Não mostrar novamente e, em seguida, selecione **Não**.
5. Feche a caixa de diálogo de salvamento de senha na parte inferior selecionando "Nunca" para não salvar as credenciais de administradores globais padrão em seu navegador.
6. No painel de navegação esquerdo, expanda **Acesso Global Seguro** e selecione **Painel**.
7. Em **Ativar Acesso Global Seguro em seu Locatário**, selecione **Ativar**.

Você ativou o Acesso Global Seguro.

## Tarefa 2: Implantar Proxy de Aplicativo

O Acesso Global Seguro é baseado no Proxy de Aplicativo, que permitirá que você crie um ponto de extremidade de nuvem seguro para seus recursos locais. Nesse caso, você permitirá que o servidor de teste configurado anteriormente se comunique por meio da infraestrutura de proxy.

1. Entre na **VM do Servidor 1** (LON-SC2) como a conta **lon-sc1\admin**. A senha deve ser fornecida pelo seu provedor de hospedagem de laboratório.
2. Abra o **Microsoft Edge**, selecione a barra de endereços, navegue para **https://entra.microsoft.com** e faça logon no Portal do Entra ID como **Administrador MOD**admin@WWLxZZZZZZ.onmicrosoft.com (em que ZZZZZZ é sua ID de locatário exclusiva fornecida pelo seu provedor de hospedagem do laboratório). A senha do usuário deve ser fornecida pelo provedor de hospedagem do laboratório.
3. Em **Acesso Global Seguro**, no painel de navegação esquerdo, expanda **Conectar** e selecione **Conectores**.
4. Escolha **Baixar o serviço do conector**.
5.  Selecione **Aceitar os termos e baixar**.
6.  Instale o **Conector do Proxy de Aplicativo do Microsoft Azure Active Directory**.
7.  Durante o processo de instalação, você deve entrar com seu nome de usuário e senha fornecidos pelo laboratório.
8.  Abra o **CMD**, execute o comando **ipconfig** e, em seguida, anote o endereço IP.
9.  Volte para o portal do Entra e atualize a página Conectores.

Você verá a VM integrada e o endereço IP associado. Isso significa que você estabeleceu o conector.

## Tarefa 3: Criar compartilhamento no servidor de arquivos

Nesta tarefa, você criará um compartilhamento SMB no servidor de arquivos local, que será acessado por meio do GSA.

1. Você ainda deve estar na VM LON-SC2.
2. Abra o **Explorer**, navegue até a unidade C: e crie uma pasta chamada **Compartilhar**.
3. Selecione a pasta Compartilhar e abra as **Propriedades**.
4. Selecione **Compartilhamento**.
5. Selecione **Compartilhar...**.
6. Selecione **Todos** no menu suspenso e selecione **Adicionar**.
7. Selecione **Compartilhar**.
8. Selecione **Não, torne a rede a que estou conectado a uma rede privada**.

## Tarefa 4: Configurar o acesso rápido e atribuir usuário

Para que seus usuários acessem o servidor de arquivos por meio do cliente GSA, você precisa ativar o Acesso Rápido e atribuí-lo aos usuários de teste. Sem essa configuração, o usuário de teste não poderá se conectar ao servidor de arquivos.

1. No painel de navegação esquerdo, expanda **Aplicativos** e selecione **Acesso Rápido**. Insira as seguintes informações:
    - Nome: **SMB para ContosoFS**
    - Grupo de Conectores: **Padrão**
1. Selecione **Adicionar segmento de aplicativo de Acesso Rápido** e preencha as seguintes informações:
    - Tipo de destino: endereço IP
    - Endereço IP: "**IP DA VM**"
    - Portas: 445
1. Escolha **Aplicar**.
1. Selecione **Salvar** e recarregue o menu Acesso rápido.
1. À esquerda, selecione **Usuários e grupos**.
1. Selecione **Adicionar usuário/grupo**.
1. Selecione **Nenhum selecionado**.
1. Adicione **Administrador de MOD**.
1. Clique em **Selecionar** > **Atribuir**.

Você habilitou o acesso rápido para seu usuário de teste; neste caso, sua conta de administrador.

## Tarefa 5: Ingressar dispositivo no Entra ID

Para usar o Acesso Global Seguro, você precisa ingressar o ponto de extremidade do cliente no Entra ID. Caso contrário, o cliente GSA não funcionará.

1. Conecte-se à VM LON-SC1, abra o menu Iniciar e selecione **Configurações**.
2. Selecione **Contas** > **Acessar Trabalho ou Escola**.
3. Para adicionar uma conta corporativa ou de estudante, selecione **Conectar**.
4. Clique em **Entrar no dispositivo com o Entra ID**.
5. Entre com suas credenciais de **Administrador do MOD** fornecidas pelo provedor de laboratório.

Depois que o ponto de extremidade ingressar no Entra ID, você poderá usar o cliente GSA para se conectar a qualquer recurso que você esteja protegendo com o Acesso Global Seguro.

## Tarefa 6: Ativar o perfil e validar a conexão

O Acesso Global Seguro é dividido em duas partes. A parte em que você está trabalhando é chamada de Acesso Privado e protege seus recursos locais e privados, como servidores de arquivos ou aplicativos locais. Para habilitar o acesso ao servidor de arquivos, você precisa habilitar o perfil de acesso privado, que permite que os usuários acessem os recursos atribuídos a eles por meio do Acesso Rápido.

1. No menu Acesso Global Seguro no painel de navegação esquerdo do centro de administração do Microsoft Entra, expanda **Conectar** e escolha **Encaminhamento de tráfego**.
2. Marque **Perfil de acesso privado**.
3. Selecione **OK**.
4. No painel de navegação esquerdo, em **Conectar**, escolha **Download do cliente**.
5. Em Windows 10/11, selecione **Baixar cliente**.
6. Instalar o **Cliente de Acesso Global Seguro**.
7. Durante o processo de instalação, você deve assinar com o administrador do MOD.
8. Abra o **Explorer** no Windows e navegue até a barra de menus **Este computador**, selecione as reticências (...) e **Mapear unidade de rede**.
9. Pasta: `\\IP-ADDRESS\Share`Use o endereço IP anotado anteriormente.
10. Selecione **Concluir**.
11. Digite o nome de usuário e a senha locais para mapear a unidade de rede.


Você se conectou com êxito ao servidor de arquivos usando o Acesso Global Seguro.
