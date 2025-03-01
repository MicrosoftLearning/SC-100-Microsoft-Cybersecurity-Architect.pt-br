---
lab: 4
title: Exercício 3 - Prevenção contra perda de dados
---

# Laboratório 4 - Exercício 3: Prevenção contra perda de dados

A Contoso Ltd. está atualmente integrando o Tailwind Traders em seus projetos. Embora a fusão ainda esteja em andamento, ambas as empresas operam em inquilinos separados. Os funcionários da Tailwind Traders são considerados usuários externos e são recebidos como convidados para o locatário da Contoso, a fim de facilitar o compartilhamento de sites e arquivos do SharePoint. Em determinados projetos, determinados funcionários da Tailwind Traders recebem clientes Windows 11 gerenciados pela Contoso Ltd. para garantir acesso total aos recursos internos, mantendo a supervisão de segurança. O acesso aos aplicativos da área de trabalho do M365 é bloqueado para dispositivos não gerenciados, e esses usuários só podem acessar o ambiente por meio de aplicativos Web. Os dispositivos gerenciados são protegidos por meio de várias políticas no Endpoint Manager. A Contoso Ltd. implementou a Proteção de Informações do Microsoft Purview para criptografar documentos confidenciais com base no tipo de informação que eles contêm. 

Como arquiteto de segurança cibernética, você examinou recentemente várias atividades no log de atividades do Defender para Aplicativos de Nuvem e descobriu que alguns documentos marcados como confidenciais estão sendo copiados para dispositivos USB externos. Você também descobriu que os usuários são livres para armazenar todos os dados da empresa aos quais têm acesso em seus dispositivos pessoais não gerenciados. Isso representa um grande problema que precisa ser resolvido. Como solução, você criará uma política de segurança para restringir o armazenamento de dados da empresa em dispositivos pessoais não gerenciados. Isso ajudará a minimizar o risco de comprometimento de dados confidenciais.

## Parte 1: Criar uma solução (obrigatório)

Nesta tarefa, você criará um conceito para lidar com os riscos que a Contoso Ltd. está enfrentando.

### Abordagem de design

A etapa inicial envolve a análise dos requisitos com base no problema descrito, compreensão dos objetivos e definição dos requisitos.

Com base no caso de uso em questão, os seguintes requisitos podem ser descritos:

- Impedir a transferência de dados para dispositivos USB
- Limitar o acesso a dados confidenciais a partir de dispositivos não gerenciados
- Bloquear download de dados confidenciais em dispositivos não gerenciados

Na segunda etapa, examine o ambiente atual da Contoso Ltd. O Microsoft Purview e o Microsoft Defender oferecem várias soluções para gerenciar o fluxo de dados, abrangendo a Proteção de Informações do Microsoft Purview, Prevenção contra Perda de Dados, Acesso Condicional e Políticas de Retenção. Investigue quais controles já estão em vigor. Acesse vários portais para revisar as configurações e políticas atuais, determinando se os ajustes são necessários ou se novas configurações/políticas precisam ser implementadas.

A terceira fase envolve a elaboração do conceito da solução. Mediante investigação, fica evidente que nenhuma das políticas atuais atende aos requisitos definidos. Portanto, um novo conjunto de políticas é essencial.

### Solução Proposta

Criar uma política de segurança para restringir o armazenamento de dados da empresa em dispositivos pessoais não gerenciados. Isso ajudará a minimizar o risco de comprometimento de dados confidenciais. A política deve enumerar os tipos de dados considerados confidenciais e os dispositivos aceitáveis nos quais eles podem ser armazenados. Além disso, a política deve fornecer diretrizes para a transferência segura de dados para dispositivos externos. Os funcionários devem ser obrigados a assinar um acordo em que declaram sua compreensão da política e seu compromisso de aderir a ela. A política deve ser comunicada a todos os funcionários e aplicada por meio de auditorias regulares e medidas disciplinares no caso de não conformidade. Sessões regulares de treinamento também devem ser realizadas para garantir que os funcionários estejam cientes dos riscos associados ao armazenamento de dados da empresa em dispositivos pessoais e da importância de se cumprir a política. Por fim, a política deve ser revisada e atualizada regularmente a fim de garantir que ela permaneça eficaz e relevante. 

|Requisito|Solução|Plano de ação|
|----|----|----|
|Bloquear a transferência de dados para dispositivos USB|Prevenção contra Perda de Dados do Ponto de Extremidade|Bloquear a cópia para um dispositivo USB de todos os dados com um rótulo confidencial|
|Restringir o acesso a dados confidenciais de dispositivos não gerenciados|Defender para Aplicativos de Nuvem|Bloquear ações de copiar/recortar/colar dados para dispositivos não gerenciados|
|Bloquear o download de dados confidenciais em dispositivos não gerenciados|Defender para Aplicativos de Nuvem|Bloquear download de dados em dispositivos não gerenciados|

## Parte 2: Implementar a solução (opcional)

### Tarefa 1: Implantar uma política de prevenção contra perda de dados

A primeira etapa do design da solução envolve a criação de uma regra de Prevenção contra Perda de Dados para Pontos de extremidade. Você implantará uma regra de DLP para bloquear a cópia de dados em unidades USB. 

1. Entre no portal de conformidade do Microsoft Purview **https://compliance.microsoft.com** como Allan Deyoung usando sua conta de **Administrador do MOD**.
1. Se solicitado a voltar para o portal clássico de conformidade do Microsoft Purview, selecione **Alternar**.
1. No portal do Microsoft Purview, no painel de navegação à esquerda, expanda **Prevenção contra perda de dados** e, em seguida, selecione **Políticas**.
1. Na página **Políticas**, selecione **+ Criar política**.
1. Na página **Iniciar com um modelo ou criar uma política personalizada**, escolha **Personalizada**, **Política personalizada**, **Avançar**.
1. Na página **Nomear política DLP**, Insira um nome e uma descrição e selecione **Avançar**.
1. Na página **Atribuir unidades de administração**, clique em **Avançar**.
1. Na página **Escolher onde aplicar a política**, selecione apenas **Dispositivos** e **Avançar**.
1. Na página **Definir configurações de política**, clique em **Avançar**.
1. Na página **Personalizar regras avançadas de DLP**, escolha **+ Criar regra**.
1. Insira um nome e uma descrição para a regra. 
1. Em **Condições**, escolha **+ Adicionar condição** e **O conteúdo contém**.
1. Especifique as seguintes condições:

    - **O conteúdo inclui**: 
      - Selecione **Adicionar**, **Rótulos de confidencialidade** e selecione os rótulos **Pessoas confiáveis**, **Projeto — Falcon**, **Confidencial**, **Altamente Confidencial**, **Confidencial — Finanças**. Clique em **Adicionar**.
13. Em **Ações**, selecione **+ Adicionar uma ação** e selecione **Auditar ou restringir atividades em dispositivos**.
14. Especifique as seguintes ações:
   -    Em **Atividades de arquivo para todos os aplicativos**, selecione **Aplicar restrições a atividades específicas**.
      - Certifique-se de que a opção **Copiar para um dispositivo USB removível** esteja selecionada e selecione a opção **Bloquear** no menu suspenso desta configuração.
      - Deixe as outras configurações inalteradas.
15. Selecione **Salvar**.
16. Selecione **Avançar**.
17. Na página **Modo de política**, selecione **Ativar a política imediatamente**. Selecione **Avançar**.
18.  Na página **Examinar e concluir**, selecione **Enviar**.

Você implementou uma política de prevenção contra perda de dados que bloqueia qualquer cópia de dados em unidades USB.

### Tarefa 2: Integrar aplicativos ao Controle de Aplicativos de Acesso Condicional

Parte da solução é criar políticas de sessão no Defender para Aplicativos de Nuvem. As políticas de sessão oferecem uma visão abrangente dos aplicativos de nuvem por meio do monitoramento em tempo real das sessões. Essas políticas permitem ações personalizadas de acordo com a política especificada para cada sessão de usuário. Para criar uma política de sessão, o controle de aplicativos de acesso condicional precisa ser implantado em seus aplicativos. O controle de aplicativos de acesso condicional adiciona recursos de monitoramento e controle em tempo real para os seus aplicativos. Criar uma política de sessão sem integrar nenhum aplicativo ao controle de aplicativos de acesso condicional não funcionará. A primeira etapa é integrar aplicativos que você deseja proteger ao controle de aplicativos de acesso condicional. 

Há duas maneiras de integrar aplicativos ao controle de aplicativos de acesso condicional:

- Adicione um aplicativo manualmente no Portal do Microsoft Defender (Configurações > Aplicativos de nuvem > Aplicativos conectados > Aplicativos do controle de aplicativos de acesso condicional)
- Configurar uma política de acesso condicional para proteger aplicativos com o Defender para Aplicativos de Nuvem

Uma política de acesso condicional encaminha todos os aplicativos especificados na política para "Controle de aplicativos de acesso condicional do Defender para Aplicativos de Nuvem". Na próxima vez que um usuário entrar nos aplicativos especificados, o aplicativo correspondente será adicionado automaticamente ao controle de aplicativos de acesso condicional. Você pode exibir esses aplicativos no portal do Microsoft Defender. 
 
>**Dica:** antes de iniciar esta tarefa, você deve verificar os aplicativos de controle de aplicativos de acesso condicional existentes. Você notará que nenhum aplicativo foi integrado ainda. Neste estágio, tente criar uma política de sessão no Defender para Aplicativos de Nuvem e verifique as mensagens de erro que ocorrem.

Nesta tarefa, você implantará o controle de aplicativos de acesso condicional em seus aplicativos criando uma política de acesso condicional no Microsoft Entra. 

1. Entre no portal do Microsoft Entra **https://entra.microsoft.com** como Allan Deyoung usando sua conta de **Administrador do MOD**.
2. No portal do Microsoft Entra, expanda **Proteção** e selecione **Acesso Condicional**.
3. Na página **Acesso condicional | Visão geral**, selecione **Políticas** e **+ Nova política**.
4. Digite um nome para a política.
5. Em **Atribuições**, selecione **Usuários** e inclua **Todos os usuários**.
6. Em **Atribuições**, selecione **Recursos de destino** e inclua **Todos os aplicativos de nuvem**.
7. Em **Controles de acesso**, selecione **Sessão**.
8. No painel **Sessão**, selecione **Usar Controle de Aplicativos de Acesso Condicional** e selecione **Usar política personalizada...** e feche o painel **Sessão** com o botão **Selecionar**.
9. Em **Habilitar política**, selecione **Ativar**.
10. Se você receber um aviso para excluir o usuário atual da política, selecione **Entendo que minha conta será afetada por essa política. Prosseguir.**.
11. Opcionalmente, especifique as condições e os controles de concessão.
12. Selecione **Criar**.

Agora entre em um dos aplicativos Web da Microsoft, como o [Outlook](https://outlook.office365.com). O aplicativo que você usar parar entrar será integrado automaticamente ao controle de aplicativos de acesso condicional. Entre no portal do Microsoft Defender e exiba os aplicativos sob controle de aplicativos de acesso condicional.

Você criou com sucesso uma política de acesso condicional para encaminhar todos os aplicativos para o Defender para Aplicativos de Nuvem e aplicativos integrados para o controle de aplicativos de acesso condicional.

### Tarefa 3: Criar políticas de sessão no Defender para Aplicativos de Nuvem

Você criará duas políticas de sessão no Defender para Aplicativos de Nuvem para bloquear downloads de dados e restringir permissões de dispositivos não gerenciados.

1. Entre no portal do Microsoft Defender**https://security.microsoft.com** como Allan Deyoung usando sua conta de **Administrador MOD**.
1. No portal Segurança da Microsoft, selecione **Aplicativos de nuvem** > **Políticas** > **Gerenciamento de políticas**.
1. Na página **Políticas**, selecione **+ Criar política** > **Política de sessão**.
1. Na página **Criar política de sessão**, selecione o modelo de política **Bloquear download com base na inspeção de conteúdo em tempo real**.
1. Insira um nome para a política.
1. Selecione uma gravidade de política e uma categoria.
1. Digite uma descrição.
1. Em **Tipo de controle de sessão**, selecione **Controlar download de arquivo (com inspeção)**.
1. Em **Origem da atividade** na seção **Atividades que correspondem a todos os seguintes**, defina o seguinte filtro:

    - **Rótulo de dispositivo**: selecione **Não é igual a** e selecione **Compatível com o Intune**.

10. Na seção **Arquivos que correspondem a todos os seguintes**, selecione este filtro:

    - **Rótulo de confidencialidade**: selecione **Igual a** e selecione os rótulos **Confidencial**, **Altamente Confidencial** e **Confidencial — Finanças**.

11. Em **Método de inspeção**, selecione **Serviço de Classificação de Dados**, **Qualquer** e **Tipo de informação confidencial...** e selecione o tipo de informação confidencial apropriado ao qual você deseja aplicar essa política.
12. Em **Ações**, selecione **Bloquear**.
13. Selecione **Criar** para criar a política.
14. Crie uma segunda política conforme descrito acima e selecione o modelo de política **Bloquear recortar/copiar e colar com base na inspeção de conteúdo em tempo real**.
15. Em **Origem da atividade** na seção **Atividades que correspondem a todos os seguintes**, insira as informações: 

    - **Tipo de atividade**: Selecione **Igual a** e selecione **Recortar/Copiar item, Colar item**
    - **Rótulo de dispositivo**: selecione **Não é igual a** e selecione **Compatível com o Intune**

16. Desabilite **Usar inspeção de conteúdo** e selecione **Criar** para criar a política.

Você criou com sucesso duas políticas de sessão no Defender para Aplicativos de Nuvem.
