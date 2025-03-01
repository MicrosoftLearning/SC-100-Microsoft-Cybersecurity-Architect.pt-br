# Laboratório 1 - Exercício 3 - Infraestrutura Segura

A Contoso Ltd. adquiriu recentemente a Tailwind Traders, que ainda usa servidores de arquivos locais para armazenamento. Como arquiteto de segurança cibernética da Contoso Ltd., você deseja avaliar uma solução para proteger esses servidores de arquivos com seu ambiente de nuvem atual. A Tailwind Traders disponibilizou um servidor de teste (Lab VM 2) que você pode usar para a implementação do POC. Neste exercício, você configurará o servidor e o integrará à sua infraestrutura de nuvem e ambiente de segurança usando o Azure Arc e enviará logs do servidor para o Defender para Nuvem.

## Parte 1: Criar uma solução (obrigatório)

Nesta tarefa, você criará um conceito para proteger o ambiente local dentro da sua infraestrutura de nuvem.

### Abordagem de design

A etapa inicial envolve análise dos requisitos com base no cenário descrito, entendendo-se os objetivos e a definição dos requisitos.

Com base no caso de uso em questão, os seguintes requisitos podem ser descritos:

- Habilitar o Defender para Nuvem em sua assinatura
- Os servidores locais precisam ser protegidos
- Os logs devem ser armazenados, para que a Solução SIEM da Contoso possa processá-los
- Avalie o estado de conformidade dos recursos de implantação

Na segunda etapa, examine o ambiente atual da Contoso Ltd. O Defender para Nuvem envia recomendações para proteger recursos locais e de nuvem identificando etapas para melhorar a configuração e a implantação. Ao monitorar ativamente as cargas de trabalho, ele aprimora a postura geral de segurança e reduz a exposição a ameaças.

### Solução proposta

|Requisito|Solução|Plano de ação|
|----|----|----|
|Habilitar o Defender para Nuvem em sua assinatura| Defender para Nuvem | Ativar planos do Defender no Defender para Nuvem |
|Os servidores locais precisam ser protegidos | Azure Arc | Integrar o servidor local ao ambiente de nuvem |
|Os logs precisam ser armazenados, para que a Solução SIEM da Contoso possa processá-los |Defender para Nuvem, DataCollectionRules, Agente AzureMonitoring, workspace do Log Analytics | Criar uma regra de Coleta de dados para coletar logs do Servidor local da Contoso |
|Avalie o estado de conformidade dos recursos de implantação | Políticas de segurança do Defender para Nuvem| Habilite a conformidade com o NIST SP 800-53 Rev.5 e avalie seu estado de conformidade.|

## Parte 2: Implementar a solução (opcional)

### Tarefa 1: criar um workspace do Log Analytics

Nesta tarefa, você criará um workspace do Log Analytics que é necessário para hospedar os dados enviados de diferentes recursos.

1. Faça logon na VM do Cliente 1 (LON-SC1) como a conta **lon-sc1\admin**. A senha deve ser fornecida pelo seu provedor de hospedagem de laboratório.
2. Abra o **Microsoft Edge**, selecione a barra de endereços, navegue até **https://portal.azure.com** e faça logon no Portal do Azure como usuário **User1-*******@LODSUATMCA.onmicrosoft.com** (em que ****** é sua ID de locatário exclusiva fornecida pelo seu provedor de hospedagem de laboratório). A senha do usuário deve ser fornecida pelo provedor de hospedagem do laboratório.
3. Na caixa de diálogo "Permanecer conectado?", selecione a caixa de seleção "Não mostrar novamente" e, em seguida, selecione **Não**.
4. Feche a caixa de diálogo de salvamento de senha na parte inferior selecionando "Nunca" para não salvar as credenciais de administradores globais padrão em seu navegador.
5. Cancele a tela de Boas-vindas ao Microsoft Azure.
6. Selecione **Criar recurso** e procure por **workspace do Log Analytics**
7. Encontre o **bloco Workspace do Log Analytics** e selecione **Criar**.
8. Em Criar site de espaço de trabalho do Log Analytics, crie um novo **Grupo de Recursos** e nomeie-o **ContosoRG**.
9. Em Detalhes da instância, insira o nome **ContosoLA**, selecione **Leste dos EUA** para a região.
10. Selecione **Revisar e criar**
11. Selecione **Criar** para iniciar a implantação.

Você criou o workspace do Log Analytics.

### Tarefa 2: habilitar o Defender para Nuvem

Antes que o Defender para Nuvem possa aplicar proteções aos seus ativos, você precisa habilitar os planos do Defender para os tipos de recursos que deseja proteger.

1. Você ainda deve estar conectado ao portal do Azure **https://portal.azure.com**.
2. Pesquise pelo **Microsoft Defender para Nuvem** e abra-o.
3. No painel de navegação esquerdo, expanda **Gerenciamento** e selecione **Configurações de ambiente**.
4. Clique em **Expandir tudo** e selecione sua Assinatura.
5. Se a assinatura for mostrada como **não registrada**, recarregue a página.
6. Selecione as reticências (...) ao lado da assinatura e, em seguida, **Editar configurações**.
7. Em **Proteção de cargas de trabalho da nuvem** , defina o controle deslizante **Servidores** à direita como **Ativado**.
8. No início da página, selecione **Salvar**.
   
Ao habilitar o Plano para Servidores, você pode ver que o Defender para Nuvem é compatível com vários outros tipos de recursos.

### Tarefa 3: habilitar o servidor local no Azure Arc

O Azure Arc é obrigatório para que possa ser usado para enviar dados para o workspace do Log Analytics que o Defender para Nuvem usa.

1. Alterne para a VM **LON-SC2** e entre no portal Azure **https://portal.azure.com**.
2. Pesquise por **Azure Arc** e abra-o.
3. No painel de navegação à esquerda, abra **recursos do Azure Arc** e selecione **Computadores**.
4. Selecione **Adicionar/Criar** > **Adicionar computador**.
5. Selecione **Gerar script** em Adicionar um servidor único.
6. Escolha **ContosoRG** em Grupo de recursos.
7. Selecione a Região **Leste dos EUA**.
8. Selecione **Baixar e executar script**.
9. Selecione **Baixar** e execute o script em seu segundo Lab Client **LON-SC2** para integrar o servidor local ao Azure.
10. Execute o Windows PowerShell como administrador.
11. Defina a política de execução como irrestrita.
```Powershell
Set-ExecutionPolicy -ExecutionPolicy unrestricted
```
12. Copie o script de integração.
13. Quando a mensagem pop-up de autenticação for exibida, faça login com a mesma conta que você está usando no portal do Azure.
14. Aguarde até o script ser concluído com sucesso.
15. Volte para LON-SC1 e abra o Azure Arc.
16. Selecione **Computadores**, selecione **Atualizar** na parte superior da página e valide se o servidor foi implantado no Azure Arc.

Você habilitou o Azure Arc no servidor de teste e os dados devem começar a fluir para o workspace do Log Analytics. Esse processo pode levar algum tempo até que você possa ver algo no painel.

### Tarefa 4: adicionar o servidor ao Defender para Nuvem e coletar logs.

Você implantará uma regra de coleta de dados para obter logs de eventos do servidor local. A regra implantará automaticamente o agente de monitoramento no servidor e encaminhará os logs para o workspace do Log Analytics criado anteriormente.

1. Você ainda deve estar conectado ao portal do Azure **https://portal.azure.com**.
2. Abra o Defender para Nuvem, selecione a guia **Introdução** na parte superior da página.
3. Abaixo de **Adicionar servidores não Azure**, selecione **Configurar**.
4. Você encontrará o workspace do Log Analytics criado anteriormente. Ao lado dele, selecione **Atualizar**.
5. Se a atualização for concluída, selecione **+ Adicionar servidores**.
6. Selecione **Regras de coleta de dados**.
7. Selecione **Criar**.
8. - Nome da regra: ContosoDCR
   - Grupo de recursos: ContosoRG
9. Selecione **Avançar: Recursos**.
10. Selecione **Adicionar Recursos**. Expanda o escopo do grupo de recursos. Verifique o computador do Azure Arc integrado anteriormente e selecione **Aplicar**.
11. Selecione **Avançar: Coletar e entregar**.
12. Clique em **Adicionar fonte de dados**.
13. Escolha o tipo de fonte de dados **Logs de eventos do Windows**.
14. Selecione todas as opções em **Configurar os logs e níveis de eventos a serem coletados:**.
15. Selecione **Avançar: Destino**.
16. Selecione **Adicionar destino**.
17.  - Tipo de destino: Logs do Azure Monitor
     - Conta ou namespace: ContosoLA
18. Clique em **Adicionar fonte de dados**.
19. Selecione **Revisar e criar**.
20. Selecione **Criar**.

Pode levar algumas horas até que o recurso seja totalmente integrado ao Defender para Nuvem. A próxima etapa é examinar a recomendação que o Defender para Nuvem gera para esse recurso.

### Tarefa 5: adicionar padrão de conformidade regulatória

Com base na recomendação, você pode começar a proteger o recurso e atribuir políticas de segurança, por exemplo, NIST SP 800-53 Rev.5, para garantir que os recursos de Tailwind traders estejam em conformidade com nossos regulamentos de conformidade.

1. Você ainda deve estar conectado ao portal do Azure **https://portal.azure.com**.
2. Abra o Defender para Nuvem, expanda **Gerenciamento** e selecione **Configurações de ambiente**.
3. Selecione **Expandir tudo**.
4. Selecione as reticências (...) ao lado da assinatura e, em seguida, **Editar configurações**.
5. No menu de navegação à esquerda, selecione **Políticas de segurança**. Pode demorar um pouco para carregar a lista.
6. Procure por **NIST SP 800-53 Rev. 5**. Mova o controle deslizante de status para **Ativado**. 
7. Volte ao Defender para Nuvem e selecione **Conformidade regulatória**.

Devido à limitação do ambiente do laboratório, você não pode ver os recursos, bem como as recomendações de conformidade. Demora um pouco até que os recursos implantados estejam visíveis no Defender para Nuvem.

No painel Conformidade regulatória, já é possível revisar todas as avaliações com falha que aparecem no painel para entender os detalhes das recomendações.
Ao avaliar continuamente os recursos em relação a esses controles, o Defender para Nuvem identifica problemas que podem impedir a obtenção de certificações de conformidade específicas. Manter a conformidade regulatória é crucial para proteger os dados da sua organização e garantir um ambiente de nuvem seguro.
