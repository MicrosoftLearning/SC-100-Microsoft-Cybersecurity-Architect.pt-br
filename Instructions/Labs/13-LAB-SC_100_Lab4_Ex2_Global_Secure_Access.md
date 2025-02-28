# Acesso Seguro Global

Depois de configurar um servidor de monitoramento, você precisa estabelecer uma rede segura para o servidor de arquivos usando o GSA (Acesso Global Seguro). Você quer garantir que o acesso a essas máquinas seja protegido até que esses servidores de arquivos possam ser migrados para armazenamento seguro em nuvem, especialmente se a Tailwind Traders estiver trazendo servidores locais para a infraestrutura de TI da sua empresa. Você decidiu não recriar a infraestrutura de VPN da Tailwind Traders para permitir que seus funcionários acessem os servidores. 

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

|Requisito|Solução|Plano de ação|
|----|----|----|
|Habilite o acesso remoto seguro para servidores locais| Acesso Global Seguro do Entra ID | Habilitar o Acesso Global Seguro  |
|Integre à infraestrutura existente | Proxy de Aplicativo | Implantar proxy de aplicativo no servidor de arquivos da Contoso |

## Parte 2: Implementar a solução (opcional)

### Tarefa 1: Ativar o Acesso Global Seguro

A primeira etapa é ativar o Acesso Global Seguro em seu locatário.

1. Entre na VM **LON-SC1** (o ponto de extremidade do cliente) como **Administrador local**. A senha deve ser fornecida pelo provedor de hospedagem do laboratório.
1. Abra o **Microsoft Edge**, selecione a barra de endereços, navegue para **https://entra.microsoft.com** e faça logon no Portal do Entra ID como **Administrador MOD**admin@WWLxZZZZZZ.onmicrosoft.com (em que ZZZZZZ é sua ID de locatário exclusiva fornecida pelo seu provedor de hospedagem do laboratório). A senha do usuário deve ser fornecida pelo provedor de hospedagem do laboratório.
1. Na caixa de diálogo **Permanecer conectado?**, selecione a caixa de seleção **Não mostrar novamente** e, em seguida, selecione **Não**.
1. Na caixa de diálogo **Salvar senha**, selecione **Agora não**.
1. Se aparecer a caixa de diálogo **Entrar no Microsoft Edge**, selecione **Não, obrigado**.
1. Se você vir uma caixa de informações no canto superior direito da tela que diz **Gerenciar autenticação multifator**, feche-a selecionando o **X**.
1. No painel de navegação esquerdo, expanda **Acesso Global Seguro** e selecione **Painel**.
1. Em **Ativar Acesso Global Seguro em seu Locatário**, selecione **Ativar**.

Você ativou o Acesso Global Seguro.

### Tarefa 2: Habilitar o TLS e instalar o conector de rede privada

O conector de rede privada é um agente leve instalado em um Windows Server, em seu ambiente local, que tem acesso aos recursos e aplicativos de back-end e é usado para facilitar a conexão com o serviço Acesso Global Seguro.  O Windows Server em que o conector será instalado deve ter o TLS 1.2 habilitado antes de instalar o conector de rede privada.

1. Entre na VM do servidor, **LON-SC2**, usando a conta de **Administrador** local. A senha deve ser fornecida pelo seu provedor de hospedagem de laboratório.
1. Quando você entrar na VM, o Gerenciador do Servidor abrirá.  Você pode minimizar essa janela.
1. Antes de instalar o conector de rede privada no servidor, habilite o TLS 1.2.  Há várias maneiras de fazer isso. Para este exercício, você copiará os comandos para definir as chaves do registro em um arquivo e, em seguida, executará esse arquivo.

    1. Abra o **Microsoft Edge**.
    1. Em uma guia do navegador, insira a URL: **`https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-configure-connectors`** e pressione a tecla Enter no teclado para abrir a documentação do produto.
    1. Role para baixo até a seção **Requisitos de TLS (Transport Layer Security)** e, na caixa de código listada em **Definir chaves do Registro**, selecione **Copiar**
    1. De dentro da VM, você abrirá o Bloco de Notas. No campo de pesquisa da barra de tarefas, digite **`Notepad`** e selecione **Bloco de Notas** para abrir o aplicativo.
    1. Use **Ctrl+V** para colar o código no Bloco de Notas.  NÃO altere nada no código colado. A primeira linha de código é necessária.
    1. No Bloco de Notas, selecione **Arquivo** e **Salvar como**. 
    1. No campo **Salvar como tipo**, selecione **Todos os arquivos** na lista suspensa e, no campo **Nome do arquivo**, insira **`EnableTLS.reg`** e selecione **Salvar.**  É importante salvar o arquivo com a extensão .reg. Anote onde o documento está salvo e feche o Bloco de Notas.
    1. Na barra de tarefas, abra o **Explorador de Arquivos** e navegue até a pasta onde você salvou o arquivo (o padrão é Este PC > Documentos).
    1. Clique duas vezes no nome do arquivo, **Enable-TLS** para executá-lo.  Como você está alterando o arquivo de registro, o sistema pergunta: **Tem certeza de que deseja continuar?**  Clique em **Sim** e selecione **OK**.  
    1. Como você atualizou o registro, precisará reiniciar o servidor. Na barra de tarefas da VM do servidor, selecione o **ícone do Windows**, selecione **Energia**, selecione **Reiniciar** e selecione **Continuar**.
    1. Após a reinicialização, faça logon novamente na VM do servidor, como o Administrador local****.
    1. Minimize ou feche o Gerenciador do Servidor.
1. Abra o **Microsoft Edge**, selecione a barra de endereços, navegue até **`https://entra.microsoft.com`** e faça logon no Portal do Entra como **Administrador MOD**admin@WWLxZZZZZZ.onmicrosoft.com (em que ZZZZZZ é sua ID de locatário exclusiva fornecida pelo seu provedor de hospedagem do laboratório). A senha do usuário deve ser fornecida pelo provedor de hospedagem do laboratório.
1. Ignore as caixas de diálogo como fez na tarefa anterior.
1. No painel de navegação esquerdo, expanda **Acesso Seguro Global**, expanda **Conectar** e selecione **Conectores**.
1. Na parte superior da página Conectores de rede privada, selecione **Baixar serviço de conector**.
1. Revise as informações e selecione **Aceitar termos e baixar**.
1. Na janela de downloads no canto superior direito da página, quando o download for concluído, selecione **Abrir arquivo**.  Se a janela de downloads fechou antes que você pudesse selecionar Abrir arquivo, selecione **Explorador de arquivos** na barra de tarefas, vá para a pasta **Downloads** e execute o arquivo **MicrosoftEntraPrivateNetworkConnectorInstaller**.
1. Marque a caixa de seleção ao lado de **Concordo com os termos e condições da licença** e selecione **Instalar**.
1. Durante o processo de instalação, você deve fazer login com o nome de usuário e a senha do Administrator MOD. A instalação pode demorar alguns minutos.
1. Quando a instalação estiver concluída, clique em **Fechar** para fechar a janela de instalação e atualize a página do navegador.  Você deve ver o conector listado e ativo.
1. Na barra de pesquisa do Windows, na barra de tarefas, digite **`cmd`** e selecione **Prompt de Comando**. 
1. Na janela Administrador: Prompt de Comando, execute o comando **`ipconfig`**, anote o endereço IP privado do seu servidor e feche a janela do Prompt de Comando.

Você instalou com êxito o conector de rede privada em seu servidor local.

### Tarefa 3: Criar uma pasta no Servidor de Arquivos

Nesta tarefa, você criará um compartilhamento SMB no servidor de arquivos local que será acessado por meio do GSA.

1. Você ainda deve estar conectado ao LON-SC2.
1. Na barra de tarefas, abra o **Explorador de Arquivos**, navegue até a Unidade C: e crie uma pasta chamada **Compartilhado**.
1. Usando a tecla direita do mouse, selecione a pasta **Compartilhado** e selecione **Propriedades**.
1. Na janela Propriedades do compartilhamento, selecione a **guia Compartilhamento**.
1. Selecione **Compartilhar...**.
1. Na lista suspensa, selecione **Todos** e selecione **Adicionar**.
1. Selecione **Compartilhar**.
1. Selecione **Não, torne a rede a que estou conectado a uma rede privada**.
1. Selecione **Concluído** e **Fechar**.
1. Minimize ou feche o Explorador de Arquivos.

Você criou uma pasta compartilhada no servidor. É essa pasta e seu conteúdo que você acessará por meio do GSA.

### Tarefa 4: Configurar o acesso rápido e atribuir usuário

O Acesso Privado fornece duas maneiras de configurar os recursos privados que você deseja encapsular pelo serviço. Aplicativos Acesso rápido ou Acesso Global Seguro. Para este exercício, você usará o Acesso Rápido.

O Acesso Rápido é o grupo principal de FQDNs e endereços IP que você deseja proteger. Ao configurar o Acesso Rápido, você está criando um novo aplicativo empresarial que serve como um contêiner para os recursos privados que você deseja proteger.

Para que seus usuários acessem os recursos do servidor de arquivos por meio do cliente GSA, você precisa ativar o Acesso Rápido e atribuí-lo aos usuários de teste.

1. Você pode ficar na VM LON-SC2 para esta etapa.
1. No painel de navegação esquerdo, expanda **Acesso Global Seguro**, expanda **Aplicativos** e selecione **Acesso Rápido**. Insira as seguintes informações:
    - Nome: **`SMB to ContosoFS`**
    - Grupo de Conectores: **Padrão**
1. Selecione **Adicionar segmento de aplicativo de Acesso Rápido** e preencha as seguintes informações:
    - Tipo de destino: **endereço IP**
    - Endereço IP: o endereço IP privado do seu servidor que você anotou na etapa anterior, **`192.168.2.100`**.
    - Portas: **`445`**
1. Escolha **Aplicar**.
1. Selecione **Salvar**. Depois de ver o campo de status do segmento de aplicativo mostrar sucesso, atualize a página do navegador. Ao atualizar a página, a página **Acesso Rápido | Propriedades de acesso à rede** abrirá.
1. À esquerda, selecione **Usuários e grupos**.
1. Selecione **Adicionar usuário/grupo**.
1. Selecione **Nenhum selecionado**.
1. Na caixa de pesquisa, insira **`MOD Administrator`** e selecione-o nos resultados da pesquisa.
1. Na parte inferior da página, pressione **Selecionar** e selecione **Atribuir**.

Você ativou o acesso rápido para seu usuário de teste.

### Tarefa 5: Ingressar dispositivo no Entra ID

Para usar o Acesso Global Seguro, você precisa ingressar o ponto de extremidade do cliente, a VM LON-SC1, no Microsoft Entra ID. Caso contrário, o cliente GSA não funcionará.

1. Volte para a VM **LON-SC1** (esta é a VM do ponto de extremidade do cliente)
1. Usando a tecla direita do mouse, selecione o ícone do Windows na barra de tarefas e selecione **Configurações**.
1. No painel de navegação esquerdo, selecione **Contas**.
1. Na página Contas, selecione **Acessar conta corporativa ou de estudante**.
1. Para adicionar uma conta corporativa ou de estudante, selecione **Conectar**.
1. Na parte inferior da janela, selecione **Ingressar dispositivo no Microsoft Entra ID**.
1. Entre com suas credenciais de **Administrador do MOD** fornecidas pelo provedor de laboratório.
1. Na janela **Confirme que esta é a sua organização**, revise as informações e selecione **Ingressar**.
1. Revise as informações na janela **Tudo pronto** e selecione **Concluído**.
1. Agora que o dispositivo ingressou no Entra ID com a sua conta de administrador do MOD, você precisa entrar usando essa conta.
    1. Na barra de tarefas, selecione o ícone do **Windows**, **Administrador** e **Trocar usuário**.
    1. No canto inferior esquerdo da janela, selecione **Outro usuário** e entre com a sua conta de administrador do MOD.
    1. Levará alguns minutos para configurar a conta e, em seguida, aparecerá uma janela **Mais informações necessárias**. Isso iniciará o processo de configuração da autenticação multifator.  Siga as instruções de configuração da MFA.

Depois que o ponto de extremidade ingressar no Entra ID, você poderá configurar o cliente GSA, que é usado para se conectar a qualquer recurso que você esteja protegendo com o Acesso Global Seguro.

### Tarefa 6: Ativar o perfil de encaminhamento de tráfego e fazer download do cliente de desktop GSA

Para habilitar o acesso a recursos ou aplicativos privados em seu ambiente local, você precisa habilitar o perfil de encaminhamento de tráfego para Acesso Privado e atribuir usuários.

Você também precisa baixar e instalar o cliente de desktop do Acesso Global Seguro.  

O tráfego de acesso privado pode ser encaminhado para o serviço conectando-se por meio do cliente de desktop Acesso Global Seguro.

1. Você ainda deve estar na **LON-SC1**, na qual você entrou com a sua conta de administrador do MOD.
1. Abra o **Microsoft Edge**. Você será solicitado a configurar o Microsoft Edge.
1. No Microsoft Edge, navegue até **`https://entra.microsoft.com`**.
1. No painel de navegação esquerdo, expanda **Acesso Global Seguro**, expanda **Conectar** e escolha **Encaminhamento de tráfego**.  Pode ser necessário expandir o painel de navegação esquerdo selecionando **>>** para visualizar as opções.
1. Selecione o botão deslizante ao lado de **Perfil de acesso privado** e selecione **OK**.
1. Agora que você habilitou o perfil de acesso privado, precisa atribuir usuários.
    1. No cartão de perfil de acesso privado, em **Atribuições de usuário e grupo**, selecione **Exibir**.
    1. Selecione onde diz **0 usuários, 0 grupos atribuídos**
    1. Selecione **Adicionar usuário/grupo**.
    1. Selecione **Nenhum selecionado**.
    1. Na barra de pesquisa, digite **`MOD Administrator`**, selecione **Administrador MOD**, pressione **Selecionar** e selecione **Atribuir**.
1. No painel de navegação esquerdo, em **Conectar**, escolha **Download do cliente**.
1. Em Windows 10/11, selecione **Baixar cliente**.
1. Na janela Downloads, selecione **Abrir arquivo**. Se a janela de downloads fechou antes de você poder selecionar Abrir arquivo, selecione **Explorador de arquivos** na barra de tarefas, vá para a pasta **Downloads** e execute o arquivo **GlobalSecureAccessClient**.
1. Selecione **Eu concordo com os termos e condições** e, em seguida, selecione **Instalar**. Na janela Controle de Conta de Usuário exibida, selecione **Sim**.
1. Quando a instalação for concluída com êxito, clique em **Fechar** para fechar a janela.
1. Na barra de tarefas, selecione a seta para cima para mostrar os ícones ocultos.  Aqui você verá o ícone do cliente Acesso Global Seguro. Se não houver uma marca de seleção verde, clique com o botão direito do mouse no ícone e selecione **Ativar**. Pode levar vários minutos para que apareça uma marca de seleção verde, que indica que está conectado.
1. Na barra de tarefas, selecione **Explorador de Arquivos** e navegue até **Este PC**. Selecione as reticências (**...**) e selecione **Mapear unidade de rede**.
1. No campo Usuário, insira `\\192.168.2.100\Share`. Use o endereço IP anotado anteriormente E selecione **Conectar usando credenciais diferentes**.
1. Selecione **Concluir**.
1. Para mapear a unidade de rede, use as credenciais da conta de administrador local no LON-SC2.  
    1. Campo de e-mail: **`Administrator`** (pode variar de acordo com o provedor de hospedagem do laboratório).
    1. Campo de senha: **`Pa55w.rd`** (pode variar de acordo com o provedor de hospedagem do laboratório).
    
    >[!NOTE] Reconhece-se que usar a conta de administrador local não é um cenário típico. Ele é usado neste exercício devido ao ambiente local simplificado. Em um cenário mais realista, com um ambiente local mais completo, o usuário teria que acessar os recursos privados com sua conta do Entra ID.

1. Antes de passar para o próximo laboratório, é recomendável trocar de usuário para obter o tamanho ideal de tela.
    1. Na barra de tarefas, selecione o ícone do **Windows**, selecione **Administrador MOD** e, em seguida, selecione **Alternar usuário**.
    1. No canto inferior esquerdo da janela, selecione **Administrador** e faça login com sua conta de administrador local.

Você se conectou com êxito ao servidor de arquivos usando o Acesso Global Seguro.
