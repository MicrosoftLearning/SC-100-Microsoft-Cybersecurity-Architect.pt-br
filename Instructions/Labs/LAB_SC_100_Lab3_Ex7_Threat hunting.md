---
lab: 3
title: Exercício 7 — Busca de ameaças
---


# Laboratório 3 — Exercício 7 — Pesquisa de Conteúdo do Microsoft Purview

Sua empresa está enfrentando uma séria ameaça à sua integridade e segurança. Um número significativo de emails maliciosos foi detectado. Sua tarefa é identificar os endereços do remetente ou as linhas de assunto desses emails. Depois de identificar esses emails maliciosos, você deve excluí-los em massa.

## Parte 1: Criar uma solução (obrigatório)

### Abordagem de design

O primeiro passo é identificar emails maliciosos. Portanto, uma análise do fluxo de correspondência atual é essencial. O Portal do Microsoft Defender fornece uma visão geral abrangente de todo o fluxo de emails de entrada e saída, juntamente com outros recursos para investigar esse tráfego. A ação de correção envolve a exclusão dos emails maliciosos. 

### Solução Proposta

|Requisito|Solução|Plano de ação|
|----|----|----|
|Identifique os emails maliciosos|Microsoft Defender para Office 365|Investigar o fluxo de emails e analisar cabeçalhos de email|
|Eliminação de riscos provenientes de emails maliciosos|Microsoft Defender para Office 365|Excluir emails maliciosos|

### Tarefa 1: Investigar emails maliciosos

Você investigará os emails de entrada no portal do Microsoft Defender e identificará quais emails são suspeitos e contêm conteúdo malicioso.

1. Entre no portal do Microsoft Defender**https://security.microsoft.com** como Allan Deyoung usando sua conta de **Administrador MOD**.
1. No portal de Segurança da Microsoft, expanda **Email e colaboração** e selecione **Explorer**.
1. Na página **Explorer**, ajuste o período de tempo da consulta para exibir todo o fluxo de emails dos últimos 30 dias e selecione **Atualizar**
1. O resultado mostra todos os emails recebidos e enviados. Investigue o fluxo de emails e o assunto dos emails.
1. Emails com o assunto “Você tem tarefas para entregar hoje” parecem suspeitos.
1. Selecione o assunto para fazer uma investigação mais aprofundada.
1. No novo painel **Você tem tarefas para serem entregues hoje**, veja as informações fornecidas e selecione **Exibir cabeçalho**.
1. No painel **Cabeçalhos de mensagem de email**, selecione **Copiar cabeçalho da mensagem** e selecione **Analisador de Cabeçalho de Mensagem da Microsoft**.
1. Uma nova guia abrirá no navegador da Web.
1. Na página **Analisador de Cabeçalho de Mensagem**, cole o cabeçalho da mensagem e selecione **Analisar cabeçalhos**.
1. Examine o resultado.

Você examinou com sucesso o fluxo de emails no portal do Microsoft Defender.

### Tarefa 2: Executar a exclusão em massa de emails maliciosos

Você chegou à conclusão de que os emails com o assunto “Você tem tarefas para serem entregues hoje” são ataques de phishing. Sua ação de correção envolve uma exclusão em massa desses emails usando o Powershell.

>[!NOTE] Você já deve ter instalado o módulo Exchange Online PowerShell. Se o módulo não estiver disponível, siga as instruções para instalá-lo.

1. Abra uma janela com privilégios elevados do PowerShell, clicando no botão Windows com o botão direito do mouse e selecionando **Windows PowerShell (Admin)**.
1. Confirme a janela **Controle de Conta de Usuário** com **Sim**.
1. Execute o seguinte cmdlet para instalar a versão mais recente do módulo PowerShell do Exchange Online:

    ```powershell
    Install-Module ExchangeOnlineManagement
    ```
1. Confirme a caixa de diálogo de segurança do repositório não confiável com **Y** para Sim e pressione **Enter**.  Esse processo pode levar algum tempo para ser concluído.
1. Abra uma janela com privilégios elevados do PowerShell, clicando no botão Windows com o botão direito do mouse e selecionando **Windows PowerShell (Admin)**.
1. Confirme a janela **Controle de Conta de Usuário** com **Sim**.
1. Insira o seguinte cmdlet para se conectar ao PowerShell de Segurança e Conformidade:

    ```powershell
    Connect-IPPSSession
    ```

1. Quando a janela **Entrar** for exibida, entre como admin@WWLxZZZZZZ.onmicrosoft.com (em que ZZZZZZ é sua ID de locatário única fornecida pelo provedor de hospedagem de laboratório) e use a senha administrativa para seu locatário.
1. Insira o seguinte cmdlet para executar a pesquisa de conteúdo e especifique o período de tempo no cmdlet:

    ```powershell
    $Search=New-ComplianceSearch -Name "Purge phishing messages" -ExchangeLocation All -ContentMatchQuery '(Received:mm/dd/yyyy..mm/dd/yyyy) AND (Subject:"You have tasks due today")'
    Start-ComplianceSearch -Identity $Search.Identity
    ```
1. Insira o seguinte cmdlet para excluir mensagens de forma irreversível:

    ```powershell
    New-ComplianceSearchAction -SearchName "Purge phishing messages" -Purge -PurgeType HardDelete
    ---
You have successfully performed a mass-deletion of malicious mails.