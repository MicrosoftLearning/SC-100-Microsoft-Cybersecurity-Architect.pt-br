---
casestudy:
  title: 'Estudo de caso: avaliar a conformidade regulatória'
  module: 'Module 4: Evaluate a regulatory compliance strategy'
---

Este exercício de estudo de caso foi projetado para fornecer experiência para executar algumas tarefas de design conceitual relacionadas aos assuntos aprendidos neste módulo.

## Estudo de caso: avaliar a conformidade regulatória

A Contoso Pharma é uma indústria farmacêutica internacional com presença na América do Norte e na Europa. A Contoso Pharma tem cargas de trabalho locais e no Azure. O objetivo é que, nos próximos dois anos, todas as cargas de trabalho estejam totalmente no Azure e haja cargas de trabalho mínimas no local. Abaixo está uma lista de suas principais cargas de trabalho:

- VMs (Windows e Linux)
- Contas de armazenamento
- Key Vault
- SQL PaaS e SQL em VMs

A Contoso Pharma também tem uma VPN site a site entre a sede em Redmond e o escritório principal em Londres. Essa VPN é usada para permitir que os recursos locais se comuniquem.

A Contoso Pharma tem um ambiente herdado em Redmond composto por alguns Windows Server 2012 executando um Servidor Web que é usado pelo aplicativo que consulta o banco de dados para verificar as informações do cliente. Após a investigação, foi observado que a comunicação do servidor Web herdado com o banco de dados é feita por meio de HTTP.

### Requisitos de design

A Contoso Pharma tem diferentes necessidades de conformidade de acordo com suas cargas de trabalho, conforme mostrado na tabela abaixo:

| **Carga de trabalho** | **Tipo de dados** | **Padrão de conformidade** |
|:---:|:---:|:---:|
| VMs Windows | Informações do titular do cartão de crédito | PCI DSS |
| SQL PaaS | Informações de integridade do paciente | HIPAA |
| Contas de Armazenamento | Informações do titular do cartão de crédito | Contas PCI DSS |

Para estar em conformidade com esses padrões, a Contoso Pharma deve ser capaz de:

- Monitorar o progresso da conformidade ao longo do tempo
- Proibir proprietários de carga de trabalho de provisionar recursos que não estejam em conformidade com esses padrões
- Verificar se as novas assinaturas implantadas no ambiente estão usando os padrões necessários por padrão
- Verificar se os recursos provisionados em cada localização geográfica mantêm os dados na região de origem para fins de soberania de dados

### Tarefas de design

* Para garantir que a Contoso Pharma possa analisar seu status de conformidade ao longo do tempo, qual ferramenta deve ser utilizada? Selecione a opção mais adequada.
* Qual serviço no Azure deve ser usado para impor aos proprietários de carga de trabalho que criem apenas recursos que estejam seguindo os padrões exigidos?
* Qual opção deve ser utilizada para garantir que, quando os proprietários da carga de trabalho criarem recursos, eles mantenham os dados na localização geográfica correta?
* Como a Contoso Pharma pode validar se as VMs que foram provisionadas estão em conformidade com o PCI DSS e, se não estiverem, o que precisa ser feito para remediar isso?
* A criptografia de dados é um componente imperativo para atender aos seus requisitos de privacidade. Quais são os estágios de dados que você deve aplicar a criptografia?
* Qual serviço do Azure você pode usar para impor a criptografia de dados entre cargas de trabalho?
