# Configurar o Entra ID

Você é Allan Deyoung, recém-promovido especialista em segurança de TI da Contoso Ltd. Como a empresa adquiriu recentemente a Tailwind Traders, você revisou seu locatário do Entra ID e decidiu aplicar novos requisitos de segurança. Sua tarefa é gerenciar as tarefas e implementar políticas para atender aos requisitos que acompanham a aquisição.

Você analisou os aplicativos empresariais e observou que alguns usuários forneceram permissões para que um aplicativo de terceiros acessasse seus respectivos dados de caixa de correio. Este é um risco potencial de perda de dados de correspondência por e-mail. Portanto, você deseja restringir esse comportamento, mas permitir que os usuários entrem e compartilhem IDs de logon em sites validados pela Microsoft. Você também deseja permitir que os usuários solicitem acesso específico a novos produtos SaaS usando sua identidade Entra ID. 

Como uma organização parceira foi atacada recentemente por meio de interceptação de SMS, você deseja impor garantia de autenticação seguindo o NIST. Para conseguir isso, você criará uma política de autenticação para desativar o SMS OTP e restringir o uso de métodos de autenticação AAL1 em sua organização. Você criará essa configuração no portal do Entra ID.

## Parte 1: Criar uma solução (obrigatório)

Nesta tarefa, você criará um conceito para lidar com os riscos que a Contoso Ltd. está enfrentando.

### Abordagem de design

A etapa inicial envolve a análise dos requisitos com base no problema descrito, o entendimento dos objetivos e a definição dos requisitos.

Com base no caso de uso em questão, os seguintes requisitos podem ser descritos:

- Restringir o acesso não controlado de aplicativos de terceiros
- Permitir que os usuários compartilhem IDs de login com serviços validados
- Permitir que os usuários solicitem acesso a produtos SaaS
- Melhorar a força da autenticação

Na segunda etapa, examine o ambiente atual da Contoso Ltd. O Microsoft Entra ID oferece soluções para gerenciar e restringir o acesso de usuários e aplicativos em nuvem com o uso de políticas Entra ID. Investigue quais controles existem e quais políticas já estão em vigor. Use o portal Entra ID para revisar as configurações e políticas atuais e determinar se ajustes são necessários ou se novas políticas precisam ser implementadas.

A terceira fase envolve a elaboração do conceito da solução. Mediante investigação, fica evidente que nenhuma das políticas atuais atende aos requisitos definidos. Portanto, ajustes na configuração do Entra ID são essenciais.

### Solução proposta

|Requisito|Solução|Plano de ação|
|----|----|----|
|Bloqueie o acesso não controlado de aplicativos de terceiros|Política de aplicativos do Entra ID|Restringir consentimento dos usuários a permissões classificadas como "baixo impacto", para aplicativos de fornecedores verificados ou aplicativos registrados nesta organização.|
|Permitir que os usuários compartilhem IDs de login com serviços validados|Política de aplicativos do Entra ID|Restringir consentimento dos usuários a permissões classificadas como "baixo impacto", para aplicativos de fornecedores verificados ou aplicativos registrados nesta organização.|
|Permitir que os usuários solicitem acesso a produtos SaaS|Política de aplicativos do Entra ID|Definir usuários que estão qualificados para aprovar aplicativos que sejam seguros para uso|
|Restringir o uso de métodos de autenticação inseguros|Métodos de autenticação do Entra ID|Criar um nível de força de autenticação que exclua os métodos SMS e Voz|

## Parte 2: Implementar a solução (opcional)

**Observação:** essas etapas de laboratório devem ser executadas no perfil de laboratório M365.

### Tarefa 1 – Restringir o uso de aplicativos de terceiros aos serviços verificados da Microsoft

Nessa tarefa, você restringirá o nível de acesso que um usuário pode conceder aos aplicativos. Você também adicionará a funcionalidade para que os usuários solicitem acesso que não podem permitir a si mesmos. 

1. Faça logon na VM do Cliente 1 (LON-Sc1) como a conta **lon-sc1\admin** . A senha deve ser fornecida pelo seu provedor de hospedagem de laboratório.
1. Abra o **Microsoft Edge**, selecione a barra de endereços, navegue até **`https://entra.microsoft.com`** e entre no Portal do Entra ID como **Administrador do MOD**admin@WWLxZZZZZZ.onmicrosoft.com (em que ZZZZZZ é sua ID de locatário exclusiva fornecida pelo seu provedor de hospedagem do laboratório). A senha de administrador deve ser fornecida pelo seu provedor de hospedagem do laboratório.
1. Se você for solicitado a configurar a autenticação multifator, siga as instruções.
1. Na caixa de diálogo **Permanecer conectado?** selecione a caixa de seleção **Não mostrar novamente** e, em seguida, selecione **Não**.
1. Feche a caixa de diálogo de salvamento de senha selecionando **Agora não**, para não salvar as credenciais do administrador global padrão em seu navegador.
1. No painel de navegação esquerdo, navegue até **Aplicativos de identidade** > **** > **Aplicativos corporativos** > **Segurança** > **Consentimentos e permissões**.
1. Navegue até **Classificações de permissão**.
1. O Entra irá sugerir as permissões mais usadas para permissões **de baixo risco** .
1. Verifique todas essas permissões e selecione **Sim, adicionar permissões selecionadas** para classificá-las como **de baixo risco** em seu locatário do Entra ID.
1. Navegue até **Configurações de consentimento do usuário**.
1. Em **Consentimento do usuário para aplicativos**, selecione a opção recomendada **Permitir o consentimento do usuário para aplicativos de editores verificados, para permissões selecionadas**. Isso permite que os usuários concordem com permissões classificadas como de "baixo impacto" (que você selecionou anteriormente) para aplicativos de editores verificados.
1. Selecione **Salvar**.
1. Navegue até **Configurações de consentimento do administrador** e habilite as Solicitações de consentimento do administrador selecionando **Sim** para permitir que os usuários solicitem o consentimento do administrador para aplicativos aos quais eles não conseguem consentir.
1. Selecione **+ Adicionar usuários** para adicionar **`Lidia Holloway`** e **`MOD Administrator`** como usuários que podem revisar as solicitações de consentimento do administrador.
1. Selecione **Salvar** na janela **Configurações de consentimento do administrador**.
1. Deixe esta guia do navegador aberta para a próxima tarefa.

Você configurou as configurações de consentimento do aplicativo que limitam o acesso que cada usuário pode conceder aos aplicativos. Os usuários ainda podem solicitar consentimento de permissão para aplicativos e a equipe de administração do aplicativo pode aprová-los depois de avaliar a necessidade e o risco do aplicativo específico.

### Tarefa 2 – Criar um nível de autenticação

Nesta tarefa, você usará o portal Entra ID para criar um nível de autenticação próprio para restringir o uso de SMS OTP na sua organização. 

1. Você ainda deve estar registrado no portal Entra ID **https://entra.microsoft.com**.
2. No painel de navegação esquerdo, navegue até **Proteção** > **Métodos de autenticação de ** > **Pontos fortes de autenticação**.
3. Selecione **Novo nível de autenticação**.
4. Insira o nome **MFA protegido**.
5. Marque as opções **MFA resistente a phishing**, **MFA sem senha** e **autenticação multifator**.
6. Em Autenticação multifator, desmarque o seguinte:
   - **Senha de acesso temporária (multiuso)**
   - **Senha + SMS**
   - **Senha + Voz**
   - **Fator único federado + SMS**
   - **Fator único federado + Voz**
7. Selecione **Avançar**.
8. Revise e verifique se nenhum dos fatores acima está faltando no nível de autenticação.
9.  Selecione **Criar**.

Você criou um nível de autenticação que restringe o uso de SMS OTP como fator de autenticação.
