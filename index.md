---
title: Instruções online hospedadas
permalink: index.html
layout: home
---

# Diretório de conteúdo

Hiperlinks para cada estudo de caso estão listados abaixo.


## Os estudos de caso foram reorganizados para a atualização de conteúdo de maio de 2023

{% assign casestudy= site.pages | where_exp:"page", "page.url contains '/Instructions/CaseStudyv2/'" %}
| Módulo | Estudo de caso |
| --- | --- | 
{% for activity in casestudy %}| {{ activity.casestudy.module }} | [{{ activity.casestudy.title }}]({{ site.github.url }}{{ activity.url }}) |
{% endfor %}


## Organização antiga de estudos de caso

{% assign casestudy= site.pages | where_exp:"page", "page.url contains '/Instructions/CaseStudy/'" %}
| Módulo | Estudo de caso |
| --- | --- | 
{% for activity in casestudy %}| {{ activity.casestudy.module }} | [{{ activity.casestudy.title }}]({{ site.github.url }}{{ activity.url }}) |
{% endfor %}