---
title: Uma dúvida de boas-vindas -> "apt" ou "apt-get"?
date: 2023-02-01 04:50:20 +0500
author: <author_id>
categories: [Linux, Infraestrutura]
tags: [linux, terminal, sistema operacional, cli, linha de comando, debian, ubuntu]     # TAG names should always be lowercase
---

<p style="text-align:justify"> Antes de qualquer coisa, sejam bem-vindos ao primeiro post aqui do blog! Vamos começar tratando de uma dúvida que atinge bastante os iniciantes no sistema operacional <strong>Linux</strong>. Afinal, qual é o comando correto que devemos utilizar para gerenciar pacotes de software no linux <i>Debian</i> e suas distribuições derivadas (ex. Ubuntu, Kali, Mint, etc)? Então segue o post até o final para entender melhor sobre os comandos <code class="language-plaintext highlighter-rouge">apt</code> e <code class="language-plaintext highlighter-rouge">apt-get</code> e compreender os cenários de utilização ideais. </p> 

## 1. O Projeto APT

<p style="text-align:justify">Com o intuito de elaborar um software com interface de usuário capaz de gerenciar a instalação e remoção de pacotes no Debian e suas respectivas distros derivadas, a equipe de desenvolvimento do <i>The Debian Project</i> iniciou o <strong>Projeto APT</strong> (<i>Advanced Package Tools</i>) em 1998, sendo incluído na versão do <i>Debian</i> 2.1, lançada em 9 de março de 1999.</p> 

<p style="text-align:justify">O projeto se baseia em uma biblioteca contendo aplicações substanciais para o seu funcionamento. Podemos, então, citar 3 programas inclusos que lidam com esta biblioteca, que são o <code class="language-plaintext highlighter-rouge">apt-get</code>, <code class="language-plaintext highlighter-rouge">apt-cache</code> e <code class="language-plaintext highlighter-rouge">apt</code>. Lembrando que o <code>apt-cache</code> não é o foco aqui, mas vale citá-lo como menção honrosa! </p>

> Atenção! Não confunda o comando <code class="language-plaintext highlighter-rouge">apt</code> com o conjunto de ferramentas <strong>APT</strong>.
{: .prompt-warning } 


<p style="text-align:justify">Dito isso, é importante pontuar que o APT pode ser considerado como uma alternativa <i>front-end</i> moderna ao <code class="language-plaintext highlighter-rouge">dkpg</code>. A principal diferença entre este último e o APT reside no fato de que enquanto um executa ações em pacotes individuais, o outro gerencia as relações de dependências entre os pacotes e demais funções.</p>

<p style="text-align:justify">No exemplo abaixo, temos um comando <code>dpkg</code> utilizado para instalar algum pacote <i>Debian</i> (extensão.deb), como aqueles baixados manualmente na internet: </p>

```bash
dpkg -i <nome_do_pacote.deb> 
```
<p style="text-align:justify"> Caso o pacote que se deseja instalar através do comando acima tenha problemas com a ausência de dependências, o <code>dpkg</code> será finalizado e informará o erro de <i> missing dependencies</i>. O mesmo não acontece quando utilizamos os benefícios do APT. Vamos observar o seguinte comando <code>apt-get</code> abaixo:</p>

```bash
apt-get install <nome_do_pacote>
```
<p style="text-align:justify">Aqui, o <code>apt-get</code> instala ou atualiza o pacote desejado, bem como todas as suas dependências logo após a realização do download. Caso haja ausência de dependências em algum pacote, não haverá encerramento do comando, pois o APT fará o download de todas as dependências faltantes. </p>

## 2. Os comandos apt-get e apt

<p style="text-align:justify"> Conforme abordado no tópico anterior, o gerenciador de pacotes <strong>APT</strong> é o padrão-ouro do <i>Debian linux</i> e de suas distribuições, sendo sólido e confiável. Porém, para que seja possível interagir com o APT, é necessário o uso de ferramentas desenvolvidas para este fim. Ambos os comandos <code>apt-get</code> e <code>apt</code> são uns dos pacotes desenvolvidos para interagir com o gerenciador de pacotes <i>Debian</i>. Observe as diferenças entre eles na lista descritiva a seguir.</p>

<dl>
  <dt><code class="language-plaintext highlighter-rouge">apt-get</code></dt>
  <dd><p style="text-align:justify"> Considerado como a primeira interface em linha de comando desenvolvida para o APT como ferramenta interativa, possibilita a instalação, atualização, remoção e limpeza de pacotes no sistema operacional. Possui diversas variações em seus comandos que o usuário necessita lembrar, tendo uma curva de aprendizado mais elevada, o que pode gerar uma confusão ainda maior quando o usuário precisar utilizar comandos <code>apt-cache</code>, pois são bastante similares. Devido a esses e outros pequenos problemas, houve a necessidade de desenvolvimento de uma solução mais eficiente, que, no caso, foi o comando <code>apt</code>.</p></dd>
  <dt><code class="language-plaintext highlighter-rouge">apt</code></dt>
  <dd><p style="text-align:justify"> É uma interface de comando aprimorada fornecida pelo APT, buscando sanar os problemas encontrados no comando <code>apt-get</code> combinando todas as funcionalidades deste, do <code>apt-cache</code> e do <code>dpkg</code> em um único comando. O intuito do <code>apt</code> é facilitar a interação com o  APT, sendo mais <i>friendly user</i>, por exemplo, fornecendo colorização, formatação mais refinada do <i>output</i>, barra de progresso no terminal, etc. Além disso, possui recursos adicionais importantes, como os novos comandos <code class="language-plaintext highlighter-rouge">apt list</code>, que lista pacotes por critério (instalados, atualizáveis, etc) e <code class="language-plaintext highlighter-rouge">apt edit-sources</code>, permitindo editar a lista de recursos. </p></dd>
</dl>

<p style="text-align:justify"> Vimos neste tópico que ambas as ferramentas foram construídas sobre o mesmo prisma, que é a mesma biblioteca substancial ao projeto ATP, tendo funções bastante similares, mas apresentando comportamentos diferentes, já que o comando <code>apt</code> foi uma evolução positiva do <code>apt-get</code>, principalmente no quesito interação, com a proposta de preencher as expectativas dos usuários quanto ao seu funcionamento. </p>

> <p style="text-align:justify"> O comando <code class="language-plaintext highlighter-rouge">apt</code> foi introduzido nos sistemas operacionais linux <i>Debian</i> em 2014. No entanto, ele apenas ganhou notoriedade com o lançamento do <i>Ubuntu 16.04</i>, em 2016, devido à popularidade dessa distro baseada no <i>Debian</i>.</p>
{: .prompt-tip }

Talvez você esteja se perguntando: 

* O comando <code>apt-get</code> vai ficar no limbo, cancelado e em desuso? 

* Entrará na temida lista de <b>procurados da deprecated</b>? 

* O comando <code>apt</code> virou mesmo "estrelinha pop"? 

É o que saberemos no tópico seguinte.

## 3. Cenários de utilização

<p style="text-align:justify"> Para responder às perguntas acima, basta dar uma lida nos dizeres da <a href="https://debian-handbook.info/browse/stable/sect.apt-get.html" target="_blank">equipe de desenvolvimento do APT</a>: </p>  

> <p style="text-align:justify">"The APT developers reserve the right to change the public interface of this tool (<code>apt</code> to further improve it. Conversely, the public interface of apt-get is well defined and will not change in any backwards incompatible way. It is thus the tool that you want to use when you need to script package installation requests." </p>

<p style="text-align:justify"> Como a interface pública do comando <code>apt</code> está em constante mudança para aperfeiçoamento, ele não deve ser utilizado em cenários que exijam operações de sistema a nível de máquina (<i>low-level operations</i>), em shell scripting, e demais atividades que necessitem de uma interface pública estável. Ele é ideal para cenários de interação por administradores de sistema e demais contextos que exijam uma <strong>interface de linha de comandos de alto nível</strong>, ou seja, voltado para o usuário final. </p>

<p style="text-align:justify"> Então quem possui uma interface pública bem definida e estável para a realização dessas operações em que o comando <code>apt</code> não é recomendado? Quem? Ele... o querido e imutável irmão mais velho <strong><code>apt-get</code></strong>. Por não sofrer alterações que gerem incompatibilidade com versões anteriores, ser uma <strong>interface de linha de comando de baixo nível</strong> (ideal para interagir com a máquina), ele é o comando mais adequado para estes cenários. Devido a isso, está bem distante de adquirir o status de <i>deprecated</i>. Vale salientar que é o comando padrão para a elaboração de scripts em shell de maneira segura.</p>

> <p style="text-align:justify"> Evite ao máximo o uso do comando <strong><code class="language-plaintext highlighter-rouge">apt</code></strong> em <b>shell scripts</b>! Por ser uma interface de linha de comando instável, poderá causar algum efeito indesejado no sistema. Utilize-o apenas se souber o que está fazendo.</p>
{: .prompt-danger }

## 4. Conclusão

<p style="text-align:justify"> Afinal, qual dos <code>apt's</code> devemos utilizar? Ante o exposto, podemos dizer que o <strong><code class="language-plaintext highlighter-rouge">apt</code></strong> é o melhor comando para ser usado de modo geral, especialmente se você é um usuário regular do sistema operacional Linux, além de ser o comando recomendado como padrão pelas próprias distribuições <i>Debian-based</i>. </p>

<p style="text-align:justify"> Relembre que o comando <code>apt</code> reúne as funcionalidades dos demais comandos <code>apt-get</code>, <code>apt-cache</code> e <code>dpkg</code> do conjunto de ferramentas <b>APT</b>, sendo ideal para uma melhor interação com o gerenciador de pacotes do sistema.</p>

<p style="text-align:justify"> Se você necessita realizar operações específicas em que seja imprescindível o uso de uma interface de linha de comando estável, não hesite em utilizar o nosso querido comando <strong><code class="language-plaintext highlighter-rouge">apt-get</code></strong>, especialmente na confecção de <b>shell scripts</b>.</p>

Obrigado pela leitura e até a próxima postagem ☕
