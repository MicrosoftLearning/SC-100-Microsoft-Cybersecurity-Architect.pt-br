---
lab: 4
title: Exercício 4 — Segurança de Ponto de Extremidade
---

# Laboratório 4 — Exercício 4 — Segurança de Ponto de Extremidade

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

1. Entre no centro de administração do Microsoft Intune**https://intune.microsoft.com** como Allan Deyoung usando sua conta de **Administrador MOD**.
2. No Centro de administração do Microsoft Intune, selecione **Segurança do ponto de extremidade** no painel de navegação à esquerda.
3. Na página **Segurança de ponto de extremidade | Visão geral**, em **Visão geral**, selecione **Linhas de base de segurança**.
4. Na página **Segurança de ponto de extremidade | Linhas de base de segurança**, selecione **Linha de base de segurança para Windows 10 ou superior**.
5. Na página **Linhas de base de segurança de MDM | Perfis**, selecione **+ Criar perfil**.
1. Examine a descrição na folha **Criar um perfil** e selecione **Criar**.
1. Na folha **Básico**, insira um nome e uma descrição.
1. Selecione **Avançar**.
1. Na folha **Definições de configuração**, investigue as diferentes opções de configuração. Quando terminar, selecione **Avançar**.
1. Na folha **Marcas de escopo**, selecione **Avançar**.
1. Na folha **Atribuições**, em **Grupos incluídos**, selecione **Adicionar todos os usuários** e selecione **Próximo**.
1. Na folha **Revisar + Criar**, selecione **Criar**.
1. Voltar para página **Segurança de ponto de extremidade | Linhas de base de segurança**.
1. Na página **Segurança do ponto de extremidade | Linhas de base de segurança**, selecione **Linha de base de segurança do Microsoft Defender para Ponto de Extremidade**.
1. Na página **Linha de base de segurança do Microsoft Defender para Pronto de Extremidade | Perfis**, selecione **+ Criar perfil**.
1. Examine a descrição na folha **Criar um perfil** e selecione **Criar**.
1. Na folha **Básico**, insira um nome e uma descrição.
1. Selecione **Avançar**.
1. Na folha **Definições de configuração**, investigue as diferentes opções de configuração. Quando terminar, selecione **Avançar**.
1. Na folha **Marcas de escopo**, selecione **Avançar**. 
1. Na folha **Atribuições**, em **Grupos incluídos**, selecione **Adicionar todos os usuários** e **Avançar**.
1. Na folha **Revisar + Criar**, selecione **Criar**.

Você criou duas políticas de linha de base de segurança para dispositivos Windows.

### Tarefa 2: implantar antivírus em dispositivos macOS

Depois de proteger os dispositivos Windows com políticas de linha de base de segurança de ponto de extremidade, você implantará um antivírus e habilitará a criptografia em dispositivos macOS para preparar seu ambiente para fusão com a Trailwind Traders.

1. Você ainda deve estar conectado ao centro de administração do Microsoft Intune **https://intune.microsoft.com**.
2. No Centro de administração do Microsoft Intune, selecione **Segurança do ponto de extremidade** no painel de navegação à esquerda.
3. Na página **Segurança do ponto de extremidade | Visão geral** em **Gerenciar**, selecione **Antivírus**.
4. Na página **Segurança do ponto de extremidade | Antivírus**, selecione **+ Criar política**.
5. No painel **Criar um perfil**, em **Plataforma**, selecione **macOS** e, em **Perfil**, selecione **Microsoft Defender Antivírus**.
6. Selecione **Criar**.
7. Na folha **Básico**, insira um nome e uma descrição.
8. Selecione **Avançar**
9. Na folha **Definições de configuração**, verifique se as configurações estão definidas da seguinte maneira:

#### Preferências de proteção fornecidas pela nuvem

- **Habilitar/desabilitar a proteção fornecida pela nuvem**: Habilitado (Padrão)
- **Habilitar/desabilitar envios automáticos de amostras**: Habilitado (padrão)
- **Nível da coleta de diagnóstico**: Opcional (padrão)
- **Atualização automática de inteligência de segurança**: Habilitado (Padrão)

#### Mecanismo antivírus

- **Habilitar proteção em tempo real**: Habilitado (padrão)
- **Habilitar modo passivo**: Desabilitado (padrão)
- **Fusão de exclusão**: admin_only
- Em **Configurações do tipo de ameaça,** selecione **+ Adicionar**
  - **Tipo de ameaça**: potentially_unwanted_application
  - **Ação a ser tomada**: bloquear
- **Mesclagem de configurações de tipo de ameaça**: admin_only
- **Habilitar computação de hash de arquivo**: Verdadeiro
- **Executar uma verificação após a atualização das definições**: Habilitado (padrão)
- **Nível de execução**: real_time

#### Proteção de rede

- **Nível de imposição**: bloquear
  
#### Proteção contra adulterações

- **Nível de imposição**: bloquear (padrão)

#### Preferências da interface do usuário

- **Controlar a entrada na versão do consumidor**: Habilitado (padrão)
- **Mostrar/ocultar ícone do menu de status**: Desabilitado (padrão)
- **Feedback iniciado pelo usuário**: Habilitado (padrão)

1.  Selecione **Avançar**.
2.  Na folha **Marcas de escopo**, selecione **Avançar**.
3.  Na folha **Atribuições, na caixa de** texto, insira **Todos os usuários** e selecione-a.
4.  Selecione **Avançar**.
5.  Na folha **Revisar + criar**, selecione **Salvar**.

Você configurou e implantou com sucesso o antivírus para dispositivos macOS.

### Tarefa 3: criptografar dispositivos macOS

Nesta tarefa, você criptografará dispositivos macOS.

1. Você ainda deve estar conectado ao centro de administração do Microsoft Intune **https://intune.microsoft.com**.
2. No Centro de administração do Microsoft Intune, selecione **Segurança do ponto de extremidade** no painel de navegação à esquerda.
3. Na página **Segurança do ponto de extremidade | Visão geral** em **Gerenciar**, selecione **Criptografia de disco**.
4. Na página **Segurança do ponto de extremidade | Criptografia de disco**, selecione **+ Criar política**.
5. No painel **Criar um perfil**, em **Plataforma**, selecione **macOS** e, em **Perfil**, selecione **FileVault**.
6. Selecione **Criar**.
7. Na folha **Básico**, insira um nome e uma descrição. Selecione **Avançar**.
8. Na folha **Definições de configuração** em **Criptografia**, defina as seguintes configurações:
   - **Ativar FileVault**: Sim
   - **Rotação da chave de recuperação pessoal**: 6 meses
   - **Descrição do local do caução da chave de recuperação pessoal**: para recuperar uma chave de recuperação perdida ou rotacionada recentemente, faça logon no site do Portal da Empresa do Intune usando qualquer dispositivo. Navegue até a seção Dispositivos no portal, escolha o dispositivo com o FileVault habilitado e selecione a opção para recuperar a chave de recuperação. O portal exibirá a chave de recuperação atual desse dispositivo.
   - **Número de vezes que é permitido desviar**: 3
   - **Permitir adiamento até sair**: Sim
   - **Desativar prompt na saída**: Sim
   - **Ocultar chave de recuperação**: Sim
  
9.  Selecione **Avançar**.
10. Na folha **Marcas de escopo**, selecione **Avançar**.
11. Na folha **Atribuições**, em **Grupos incluídos**, selecione **Adicionar todos os usuários**.
12. Selecione **Avançar**.
13. Na folha **Revisar + Criar**, selecione **Criar**.

Você configurou e implantou um perfil do FileVault para criptografar dispositivos macOS.