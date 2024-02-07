---
casestudy:
  title: 'Estudo de caso: práticas recomendadas com MCRA e MCSB'
  module: 'Module 11: Recommend security best practices with MCRA and MCSB'
---

Este exercício de estudo de caso foi projetado para fornecer experiência para executar algumas tarefas de design conceitual relacionadas aos assuntos aprendidos neste módulo.

## Estudo de caso: práticas recomendadas com MCRA e MCSB
 
A CONTOSO é uma empresa de serviços de saúde com sedes em Chicago, EUA, e em Londres, Reino Unido.  
A empresa fornece serviços de saúde para clientes em suas instalações em torno da área metropolitana de Chicago, EUA, e de Londres, Reino Unido.  As instalações da Contoso estão cheias de hospitais com médicos, enfermeiros e outros profissionais da saúde. A Contoso iniciou uma migração em toda a empresa de todos os serviços essenciais para a nuvem. Essa migração inclui servidores locais, VMs e dispositivos de gerenciamento e monitoramento de suporte.

A Contoso iniciou sua migração para a nuvem, com exceção de alguns dados e aplicativos que precisam ser hospedados no local devido a requisitos normativos e de conformidade. A Contoso estabelece um locatário do Azure Active Directory (Azure AD). Esse Azure AD é sincronizado com o Serviços de Domínio do Active Directory (AD DS), que é mantido em controladores de domínio locais. À medida que a migração progride, assinaturas adicionais do Azure serão criadas conforme necessário para cada departamento, incluindo aplicativos SaaS. Para facilitar seu trabalho diário, a maioria dos funcionários tem acesso aos aplicativos do Microsoft 365.  
 
Para oferecer suporte à conectividade contínua, testes básicos de Virtual Desktop Infrastructure (VDI)  
foram iniciados para a maioria das categorias de funcionários, como gerentes de conta e equipes  
de suporte, de negócios, de finanças e de RH. A conectividade segura é apoiada por meio de um gateway de Rede  
Virtual Privada (VPN) para um conjunto limitado de usuários e dispositivos. Além disso, um  
firewall de terceiros foi implantado para proteger as Redes Locais Virtuais (VLANs)  
do servidor virtual.  
 
Enquanto estão no local com os clientes, os médicos usam dispositivos móveis com dados  
de rastreamento e monitoramento armazenados localmente. Esses dados são protegidos usando criptografia de armazenamento  
proprietária, e cada profissional de saúde é obrigado a fazer logon em seu dispositivo usando credenciais armazenadas localmente antes de acessar os dados. 
 
### Requisitos

À medida que a migração para a nuvem prossegue e se expande, a Contoso planeja mover todos os dados e aplicativos  
locais para a nuvem, com exceção dos aplicativos fora do escopo. 

* Implante o Microsoft 365 Defender e o Defender for Cloud para aprimorar a postura de segurança da Contoso contra adversários 
* O MCSB da política de conformidade da Microsoft precisa ser aplicada à Assinatura do Azure 
* A Contoso deseja buscar proativamente por ameaças em potencial e gerenciar ativamente a superfície de ataque 
* A Contoso deseja centralizar o gerenciamento de identidades tanto de contratados externos quanto de funcionários internos e pacientes 
* Todos os dispositivos de ponto de extremidade devem ser gerenciados centralmente e continuamente avaliados quanto à conformidade. 
* As Informações de Integridade Protegidas (PHI) armazenadas em dispositivos móveis usados por profissionais de saúde serão movidas para a nuvem seguindo a política de residência de dados para ficar em conformidade com os regulamentos regionais. 
* O acesso a dispositivos móveis enquanto estiver em campo deve ser restrito por geolocalização e exigir biometria como uma autenticação multifator  
* O compartilhamento de dados entre aplicativos no mesmo dispositivo deve ser controlado.  
* Conformidade com os requisitos da lei americana HIPAA (Health Insurance Portability and Accountability Act) e do NHS (National Health Services, do Reino Unido). 
* A Contoso deseja gerenciar os administradores de privilégios seguindo o princípio do menor privilégio e impor políticas de acesso just-in-time. 
* A Contoso deseja recuperar seus dados em caso de desastre e também manter esses dados de backup em um local seguro. Em caso de desastre na região primária, a Contoso deseja fazer um failover para a região secundária. 
* A Contoso quer garantir que eles sigam a abordagem de confiança zero para validar todos os acessos de entrada
* À medida que os dados e o processamento são movidos para o Azure, o gateway VPN deve ser configurado para  
aceitar conexões P2S seguras de dispositivos que executam uma variedade de sistemas operacionais  
em desktops e dispositivos móveis, incluindo Windows, macOS, Android e outros.  

### Tarefas de design

* Qual plano do Defender é necessário para que a Contoso atenda às suas necessidades de Negócios e de Segurança? 
* O que a Contoso poderia fazer para validar todos os acessos de entrada e seguir a abordagem de confiança zero ao mesmo tempo? 
* Como a Contoso poderia aplicar as políticas do NHS e da HIPAA em seu ambiente de nuvem? 
* O que a Contoso deve usar para ter visibilidade sobre todas as ameaças e vulnerabilidades existentes? 
* Como a Contoso deve implantar e manter as configurações de segurança nos dispositivos de ponto de extremidade? 
* Como a Contoso pode ter visibilidade sobre os aplicativos de nuvem usados e sobre os dados compartilhados externamente? 
