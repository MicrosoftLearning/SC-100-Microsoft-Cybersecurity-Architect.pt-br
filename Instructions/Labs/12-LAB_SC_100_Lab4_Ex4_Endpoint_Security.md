# Segurança de ponto de extremidade

A Contoso usa o Microsoft Intune para gerenciar seus dispositivos e fornece a seus funcionários dispositivos Windows 10 e Windows 11. A empresa implementou vários perfis de configuração no passado. No entanto, uma análise de infraestrutura em toda a empresa revelou que as políticas existentes foram criadas de forma independente, dificultando sua visualização holística e seu rastreamento. Como arquiteto de segurança cibernética da empresa, você decidiu consolidar todas as configurações necessárias e críticas em um só lugar. 

Além disso, a análise revelou que a Tailwind Traders usa dispositivos macOS em seu ambiente. Como parte da próxima fusão, você planeja preparar o locatário da Contoso para os novos dispositivos macOS.

## Parte 1: Criar uma solução (obrigatório)

Nesta tarefa, você criará um conceito para resolver os desafios que a Contoso Ltd. está enfrentando.

### Abordagem de design

No cenário fornecido, os seguintes requisitos podem ser descritos:

- Consolide todas as configurações para dispositivos Windows em um só lugar
- Proteger dispositivos macOS

O Microsoft Endpoint Manager, com linhas de base de segurança, gerencia e protege centralmente os pontos de extremidade, incluindo desktops, laptops, dispositivos móveis e servidores. Ele integra ferramentas como Intune e Configuration Manager, permitindo a implantação eficiente de aplicativos, imposição de políticas, conformidade e monitoramento de dispositivos. 

Uma política de linha de base de segurança compreende um conjunto de definições de configuração recomendadas pela Microsoft, detalhando suas implicações de segurança. Essas configurações são baseadas nos comentários de grupos de produtos, parceiros, clientes e equipes de engenharia de segurança da Microsoft. Essas linhas de base abrangem definições de configuração de dispositivo semelhantes às de várias políticas do Intune. A personalização de cada linha de base implantada permite a imposição das configurações e valores necessários. Ao estabelecer um perfil de linha de base de segurança no Intune, você está essencialmente criando um modelo que inclui vários perfis de configuração de dispositivo. Essas recomendações devem ser revisadas e adaptadas regularmente de acordo com os respectivos requisitos de negócios.

### Solução Proposta

|Requisito|Solução|Plano de ação|
|----|----|----|
|Consolide todas as configurações para dispositivos Windows em um só lugar|Microsoft Endpoint Manager — Segurança de Ponto de Extremidade|Implantar políticas de linha de base de segurança
|Proteger dispositivos macOS|Microsoft Endpoint Manager|Implantar antivírus em dispositivos macOS|

## Parte 2: Implementar a solução (opcional)

### Tarefa 1: Implantar políticas de linha de base de segurança de ponto de extremidade

Seu objetivo geral é proteger seus pontos de extremidade adequadamente e consolidar o maior número possível de políticas em um só lugar. Você conseguirá isso criando políticas de linha de base de segurança de ponto de extremidade para dispositivos Windows no Intune.

1. Faça logon na VM do cliente Windows **LON-SC1** com a conta de **Administrador** local. A senha deve ser fornecida pelo seu provedor de hospedagem de laboratório.
1. Entre no centro de administração Microsoft Intune **`https://intune.microsoft.com`** como **Administrador do MOD**admin@WWLxZZZZZZ.onmicrosoft.com (em que ZZZZZZ é sua ID de locatário exclusiva fornecida pelo provedor de hospedagem de laboratório). A senha do usuário deve ser fornecida pelo provedor de hospedagem do laboratório.
1. Se você vir uma caixa de informações no canto superior direito da tela que diz **Gerenciar autenticação multifator**, feche-a selecionando o **X**.
1. No Centro de administração do Microsoft Intune, selecione **Segurança do ponto de extremidade** no painel de navegação à esquerda.
1. Na página **Segurança de ponto de extremidade | Visão geral**, em **Visão geral**, selecione **Linhas de base de segurança**.
1. Na página **Segurança de ponto de extremidade | Linhas de base de segurança**, selecione **Linha de base de segurança para Windows 10 ou superior**.
1. Na página **Linha de base de segurança para o Windows 10 e posteriores | Perfis**, selecione **+ Criar perfil**.
1. Examine a descrição na folha **Criar um perfil** e selecione **Criar**.
1. Na folha **Básico**, insira:
    1. Nome: **`Secure Windows Endpoints`**
    1. Descrição: **`The Security Baseline for Windows 10 and later represents the recommendations for configuring Windows.`**.
1. Selecione **Avançar**.
1. Na folha **Definições de configuração**, investigue as diferentes opções de configuração. Quando terminar, selecione **Avançar**.
1. Na folha **Marcas de escopo**, selecione **Avançar**.
1. Na folha **Atribuições**, em **Grupos incluídos**, selecione **Adicionar todos os usuários** e selecione **Próximo**.
1. Na folha **Revisar + Criar**, selecione **Criar**.
1. Voltar para página **Segurança de ponto de extremidade | Linhas de base de segurança**.
1. Na página **Segurança do ponto de extremidade | Linhas de base de segurança**, selecione **Linha de base de segurança do Microsoft Defender para Ponto de Extremidade**.
1. Na página **Linha de base de segurança do Microsoft Defender para Pronto de Extremidade | Perfis**, selecione **+ Criar perfil**.
1. Examine a descrição na folha **Criar um perfil** e selecione **Criar**.
1. Na folha **Básico**, insira:
    1. Nome: **`Defender for Endpoint Security Baseline`**
    1. Descrição: **`Security best practices for the Microsoft security stack on devices managed by Intune`**.
1. Selecione **Avançar**.
1. Na folha **Definições de configuração**, investigue as diferentes opções de configuração. Quando terminar, selecione **Avançar**.
1. Na folha **Marcas de escopo**, selecione **Avançar**.
1. Na folha **Atribuições**, em **Grupos incluídos**, selecione **Adicionar todos os usuários** e **Avançar**.
1. Na folha **Revisar + Criar**, selecione **Criar**.

Você criou duas políticas de linha de base de segurança para dispositivos Windows.

### Tarefa 2: implantar antivírus em dispositivos macOS

Depois de proteger os dispositivos Windows com políticas de linha de base de segurança de ponto de extremidade, você implantará um antivírus e habilitará a criptografia em dispositivos macOS para preparar seu ambiente para a fusão com a Trailwind Traders.

1. Você ainda deve estar conectado ao centro de administração do Microsoft Intune **https://intune.microsoft.com**.
1. No Centro de administração do Microsoft Intune, selecione **Segurança do ponto de extremidade** no painel de navegação à esquerda.
1. Na página **Segurança do ponto de extremidade | Visão geral** em **Gerenciar**, selecione **Antivírus**.
1. Na página **Segurança do ponto de extremidade | Antivírus**, selecione **+ Criar política**.
1. No painel **Criar um perfil**, em **Plataforma**, selecione **macOS** e, em **Perfil**, selecione **Microsoft Defender Antivírus**.
1. Selecione **Criar**.
1. Na folha **Básico**, insira:
    1. Nome: **`Deploy antivirus on macOS devices`**
    1. Descrição: **`Deploy antivirus and enable encryption on macOS devices to prepare your environment for merging with Trailwind Traders.`**
1. Selecione **Avançar**
1. Na guia **Definições de configuração**, verifique se as configurações estão definidas da seguinte maneira:
1. Em **Preferências de proteção fornecida pela nuvem**:
    - Habilitar/desabilitar proteção fornecida pela nuvem: **Habilitado (Padrão)**
    - Habilitar/desabilitar envios automáticos de amostras: **Habilitado (padrão)**
    - Nível de coleta de diagnóstico: **opcional (padrão)**
    - Atualização automática de inteligência de segurança: **Habilitado (Padrão)**
1. Em **Mecanismo antivírus**:
    - Habilitar proteção em tempo real: **Habilitado (padrão)**
    - Habilitar modo passivo: **Desabilitado (padrão)**
    - Mesclagem de exclusão: **admin_only**
1. Em **Configurações do tipo de ameaça**, selecione **+ Adicionar**:
    - Na caixa de texto Tipo de ameaça, insira: **potentially_unwanted_application**
    - Ação a ser tomada: **bloquear**
    - Mesclagem das configurações do tipo de ameaça: **admin_only**
1. Habilitar computação de hash de arquivo: **True****
1. Executar uma verificação após a atualização das definições: **Habilitado (padrão)**
1. Nível de aplicação: **real_time**
1. Em **Proteção de rede**:
    - Nível de imposição: bloquear
1. Em **Proteção contra adulterações**:
    - Nível de imposição: **bloquear (padrão)**
1. Em **Preferências da interface do usuário**
    - Controlar a entrada na versão do consumidor: **habilitado (padrão)**
    - Mostrar/ocultar ícone do menu de status: **Desabilitado (padrão)**
    - Feedback iniciado pelo usuário: **habilitado (padrão)**
1. Selecione **Avançar**.
1. Na folha **Marcas de escopo**, selecione **Avançar**.
1. Na guia **Atribuições**, na caixa de texto, insira e selecione **Todos os usuários**.
1. Selecione **Avançar**.
1. Na guia **Revisar + criar**, selecione **Salvar**.

Você configurou e implantou com sucesso o antivírus para dispositivos macOS.

### Tarefa 3: criptografar dispositivos macOS

Nesta tarefa, você criptografará dispositivos macOS.

1. Você ainda deve estar conectado ao centro de administração do Microsoft Intune **https://intune.microsoft.com**.
1. No Centro de administração do Microsoft Intune, selecione **Segurança do ponto de extremidade** no painel de navegação à esquerda.
1. Na página **Segurança do ponto de extremidade | Visão geral** em **Gerenciar**, selecione **Criptografia de disco**.
1. Na página **Segurança do ponto de extremidade | Criptografia de disco**, selecione **+ Criar política**.
1. No painel **Criar um perfil**, em **Plataforma**, selecione **macOS** e, em **Perfil**, selecione **FileVault**.
1. Selecione **Criar**.
1. Na folha **Básico**, insira:
    1. Nome: **`Encrypt macOS devices`**
    1. Descrição: **`FileVault provides built-in Full Disk Encryption for macOS devices.`**
    1. Selecione **Avançar**.
1. Na folha **Definições de configuração** em **Criptografia**, defina as seguintes configurações:
   - Habilitar FileVault: **Sim**
   - Rotação da chave de recuperação pessoal: **6 meses**
   - Descrição do local do depósito da chave de recuperação pessoal: **`To recover a lost or recently rotated recovery key, log in to the Intune Company Portal website using any device. Navigate to the Devices section within the portal, choose the device with FileVault enabled, and then select the option to retrieve the recovery key. The portal will display the current recovery key for that device.`**
   - Número de vezes que é permitido desviar: **3**
   - Permitir adiamento até sair: **Sim**
   - Desabilitar prompt na saída: **Sim**
   - Ocultar chave de recuperação: **Sim**
   - Selecione **Avançar**.
1. Na folha **Marcas de escopo**, selecione **Avançar**.
1. Na folha **Atribuições**, em **Grupos incluídos**, selecione **Adicionar todos os usuários** e **Avançar**.
1. Na folha **Revisar + Criar**, selecione **Criar**.

Você configurou e implantou um perfil do FileVault para criptografar dispositivos macOS.
