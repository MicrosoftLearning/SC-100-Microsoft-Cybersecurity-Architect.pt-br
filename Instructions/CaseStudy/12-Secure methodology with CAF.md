---
casestudy:
  title: 'Estudo de caso: metodologia segura com CAF'
  module: 'Module 12: Recommend secure methodology with CAF'
---
Este exercício de estudo de caso foi projetado para fornecer experiência para executar algumas tarefas de design conceitual relacionadas aos assuntos aprendidos neste módulo.

## Estudo de caso: recomendar metodologia segura com CAF

- A Contoso Banking é uma subsidiária do Grupo Contoso, que está sendo transformada em uma entidade comercial independente. A Contoso Banking será uma empresa separada com sua própria infraestrutura e organização de TI. 
- A infraestrutura da Contoso Banking será baseada inteiramente na nuvem do Microsoft Azure. Para criar uma plataforma de nuvem segura desde o início da empresa, você precisa projetar uma zona de destino do Azure segura.
- Os termos do contrato determinam que a transição deve levar no máximo 6 meses
- A Contoso Banking planeja criar uma solução FinTech de última geração usando soluções nativas da nuvem. O lançamento do MVP 1 precisa ser feito em 6 semanas.

### Requisitos

O Grupo Contoso não usa nenhum serviço de nuvem. A infraestrutura é totalmente hospedada em um data center próprio. O ambiente que fará parte da Contoso Banking inclui:

- Ambiente 1: sistemas bancários centrais (20 aplicativos). A segurança é essencial.
- Ambiente 2: aplicativo de última geração / Fintech criado no Serviço de Kubernetes do Azure e no Azure Data Lake. 100 lançamentos por mês

#### Alterações planejadas

Ambiente 1: a Contoso Banking planeja mover toda a infraestrutura bancária principal para a nuvem. A abordagem deve incluir o seguinte:

- Implantar uma zona de destino onde os aplicativos principais estão hospedados.
- Usuários precisam acessar os principais aplicativos a partir de estações de trabalho seguras baseadas em nuvem. Usuários precisam ter uma experiência consistente para acessar os aplicativos.
- A solução precisa garantir que as práticas recomendadas de gerenciamento de identidade e acesso, governança, segurança, rede e registro em log sejam seguidas.

O Ambiente 2 (aplicativo Fintech) precisa atender aos seguintes requisitos:

- 100 lançamentos por mês
- Estar sempre pronto para auditoria
- Estar em conformidade com PCI-DSS

### Tarefas de design

- Quais são os componentes necessários para implantação na zona de destino?
- Como a escolha das cargas de trabalho afetará o tempo e a complexidade da implementação?
- Como você implementaria o acesso seguro aos aplicativos principais?
- Qual zona de destino do Azure você deve recomendar que a Contoso Banking implemente para o Ambiente 1?
- Qual zona de destino do Azure você deve recomendar que a Contoso Banking implemente para o Ambiente 2?
