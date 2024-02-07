---
casestudy:
  title: 'Estudo de caso: estratégia contra ransomwares'
  module: 'Module 13: Recommend a ransomware strategy by using Microsoft Security Best Practices'
---
Este exercício de estudo de caso foi projetado para fornecer experiência para executar algumas tarefas de design conceitual relacionadas aos assuntos aprendidos neste módulo.

## Estudo de caso: recomendar uma estratégia contra ransomwares usando as práticas recomendadas de segurança da Microsoft
 
A CONTOSO é uma empresa de serviços de saúde com sedes em Chicago, EUA, e em Londres, Reino Unido.  
A empresa fornece serviços de saúde para clientes em suas instalações em torno da área metropolitana de Chicago, EUA, e de Londres, Reino Unido.  As instalações da Contoso estão cheias de hospitais com médicos, enfermeiros e outros profissionais da saúde. A Contoso iniciou uma migração em toda a empresa de todos os serviços essenciais para a nuvem. Essa migração inclui servidores locais, VMs e dispositivos de gerenciamento e monitoramento de suporte.

A Contoso iniciou sua migração para a nuvem, com exceção de alguns dados e aplicativos que precisam ser hospedados no local devido a requisitos normativos e de conformidade. A Contoso tem um locatário Azure Active Directory (Azure AD). Esse Azure AD é sincronizado com o Serviços de Domínio do Active Directory (AD DS), que é mantido em controladores de domínio locais. À medida que a migração progride, assinaturas adicionais do Azure serão criadas conforme necessário para cada departamento, incluindo aplicativos SaaS. Para facilitar seu trabalho diário, a maioria dos funcionários tem acesso aos aplicativos do Microsoft 365.  
 
Houve vários casos recentes de ransomware de alto perfil envolvendo concorrentes da Contoso no mercado de serviços de saúde. O CEO e o CISO estão preocupados já que a Contoso ainda não ter um plano em vigor para mitigar o risco de um ataque de ransomware. O CISO solicitou pessoalmente que você elabore um plano de resposta e mitigação contra ransomwares para apresentar aos executivos da empresa em duas semanas. Alguns dos funcionários de TI mais experientes acreditam que a ameaça de ransomwares está sendo exagerada e que tudo o que a empresa realmente precisa é de bons backups e uma segurança sólida no perímetro.
 
### Requisitos

* O plano de resposta e mitigação contra ransomware deve incluir não apenas infraestruturas críticas locais e serviços em nuvem, mas também dados da empresa armazenados em laptops e dispositivos móveis da empresa usados por funcionários em campo
* O CEO e o CISO adotaram uma abordagem linha-dura: nunca negociarão ou pagarão hackers de ransomware. Eles disseram que, no caso de um ataque de ransomware, o objetivo é restabelecer a operação de sistemas críticos dentro de 12 horas e a funcionalidade completa em 48 horas.
* As estratégias de tratamento de dados devem estar em conformidade com os requisitos de privacidade, incluindo a HIPAA nos EUA e padrões similares no Reino Unido.
* Seu plano também deve detalhar por que um bom backup não é o suficiente para mitigar a ameaça de ransomwares.

### Perguntas iniciais

* Quais departamentos e pessoal precisam estar envolvidos na criação do plano de mitigação contra ransomwares? 
* Quais serviços e elementos da infraestrutura precisam ser abordados pelo plano? 
* Quais cronogramas são realistas para criar um plano robusto de resposta contra ransomwares?
* Quais são as principais providências para o sucesso da implementação do seu plano de proteção contra ransomwares?

### Tarefas de design

* Listar os serviços do Azure e do M365 será fundamental para fazer backup e proteger seus dados. Explique por que cada serviço é uma parte importante da resposta contra ransomwares e os pontos negativos de cada um.
* Anote todas as necessidades especiais de sua empresa que não são abordadas pelas soluções já existentes do Azure e do M365.
* Liste os serviços e elementos da infraestrutura que precisam ser abordados pelo plano.
* Estime alguns cronogramas realistas para criar e executar um plano robusto de resposta contra ransomwares. 