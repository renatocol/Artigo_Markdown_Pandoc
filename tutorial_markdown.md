## Tutorial para edição de artigo acadêmico com Markdown, Pandoc, LaTeX e Zotero

### Autor: Renato Perim Colistete, FEA-USP

*Última atualização: 14/7/2021*


Este tutorial apresenta os passos básicos para a preparação de artigos acadêmicos utilizando [Markdown](https://en.wikipedia.org/wiki/Markdown), uma sintaxe simples e versátil de formatação de textos com amplo uso em webpages, editores de programação, GitHub/GitLab e Jupyter Notebook. Por meio do [pandoc](https://pandoc.org/MANUAL.html), o texto básico em Markdown é convertido em pdf com todas as funcionalidades do [LaTeX](https://www.latex-project.org/), além de outros formatos como odt e docx. O workflow é integrado com o gerenciador de bibliografia [Zotero](https://www.zotero.org/). O sistema é uma alternativa à redação de textos acadêmicos com o Word ou editores como Overleaf, utilizando LaTeX.

#### Instalações necessárias

Requer-se a instalação prévia de quatro programas: um editor Markdown, o gerenciador de bibliografia Zotero, o sistema de preparação de documentos LaTeX e o módulo de conversão de documentos, pandoc. Toda a apresentação a seguir utiliza o [Typora](https://typora.io/), um ótimo editor de Markdown, que conta com vários recursos e funcionalidades para a redação de trabalhos acadêmicos. Recomenda-se que os programas sejam instalados em um ambiente virtual próprio, a ser criado, por exemplo, com [venv](https://docs.python.org/pt-br/3/library/venv.html#module-venv) (Python) ou [conda](https://docs.conda.io/en/latest/) (Anaconda). 

- *LaTeX*

  Instalar conforme as instruções para o seu sistema operacional: https://www.latex-project.org/get/

- *Pandoc*

  Instalar de acordo com as instruções: https://github.com/jgm/pandoc/releases/tag/2.13

- *Typora*

  Instalar de acordo com as instruções, na aba Download: https://typora.io/

- *Zotero*

  Instalar Zotero e o Zotero Connector para navegador Firefox ou Chrome/Chromium: https://www.zotero.org/download/

- *Anaconda*

  Instalar de acordo com as instruções: https://docs.anaconda.com/anaconda/installMarkdown

Dois bons guias gerais sobre Markdown são o [Markdown-Guide](https://markdown-guide.readthedocs.io/en/latest/basics.html) e a [Introdução do Programming Historian](https://programminghistorian.org/pt/licoes/introducao-ao-markdown). O Typora, editor usado neste tutorial, baseia-se em uma das variantes (flavors) do Markdown puro, o [GitHub Flavored Markdown](https://help.github.com/articles/github-flavored-markdown/). O [Markdown Reference](https://support.typora.io/Markdown-Reference/) do Typora contém todos os detalhes da sintaxe e é também um bom guia geral da linguagem. Para o Zotero, ver [Quick Start Guide](https://www.zotero.org/support/pt/quick_start_guide) e [Tutorial Zotero 5.0](https://www.iel.unicamp.br/arquivos/biblioteca/TUTORIAL_zotero_v1.pdf).

#### Instalação da biblioteca ZoteroBetterBibTeX no Zotero

O plugin [Better BibTeX for Zotero](https://retorque.re/zotero-better-bibtex/) permite integrar o texto Markdown com Zotero por meio de uma "citation key" que é gerada para cada item da bibliografia com o formato @authortitleyear (p. ex., @canabravaAcucarNasAntilhas1981). Os passos a seguir baseiam-se no [tutorial de Simon Lindgren](https://www.simonlindgren.com/notes/2019/11/15/setup-for-writing-in-markdown-citing-with-zotero-and-publishing-with-pandoc):

- Abrir o Zotero.
- Para este tutorial, faça primeiro o download do arquivo biblio.bib que se encontra na pasta "bibliografia", nesta página do GitHub. Crie um diretório em seu computador e salve biblio.bib nele. Para facilitar, nomeie este diretório no seu computador como "artigo", que será o nome que utlizaremos ao longo do tutorial.
- Faça o download do ZoteroBetterBibTeX em https://github.com/retorquere/zotero-better-bibtex/releases/
- Para executar o download do ZoteroBetterBibTeX, clique o botão direito do mouse no arquivo xpi da última versão do pacote e salve em algum diretório temporário.
- Instale o arquivo xpi no Zotero: Ferramentas >> Extensões >> clique na janela no alto à direita >> Install Add-on from file. Localize o arquivo xpi salvo no seu diretório temporário e o carregue.
- No Zotero, entre em Editar >> Preferências >> Better BibTex e defina o formato da biblio em "Formato da chave de citação"; p. ex. [auth:lower][shorttitle3_3][year].
- Na janela principal do Zotero, selecione com o cursor todas as referências (da pasta que foi importada, "biblio"), clique no botão direito do mouse e selecione BetterBibTex >> Atualizar chave BibTex
- Outro passo é definir atualização automática das referências como default do Zotero: Arquivo >> Exportar a biblioteca >> Selecionar Better BibTex >> Manter atualizado. 
- Em seguida, selecionar Editar >> Preferências >> Better BibTeX >> Exportação automática >> Imediatamente

####  Começando com um texto básico

A estrutura básica do artigo acadêmico a ser editado é composta por um bloco de metadados [YAML](https://support.typora.io/YAML/) no cabeçalho, seções e bibliografia ao final (notar que o bloco YAML começa com ```---``` e termina com ```---``` ). Um primeiro exemplo é apresentado a seguir. 

- Copie e cole toda a estrutura do texto abaixo (inclusive ```---``` no início e no final dos metadados YAML) em um arquivo em branco do Typora ou outro editor Markdown. 
- Para copiar, passe o cursor no texto abaixo e clique no símbolo no alto à direita.
- Em seguida, salve este arquivo com o formato [nome].md no diretório "artigo". Aqui, chamaremos este arquivo Markdown de paper1.md.

```markdown
---
title: A Simple Example
author: Name Surname
date: day month year
---

# Heading 1

Insert one text here and add a footnote.[^1]

[^1]: The footnote is inserted here.

## Heading 2

Insert another text here and use *italics* and **bold**.

A quotation in a footnote is very simple [@canabravaAcucarNasAntilhas1981, p. 15].

Add another text and quote a different author [@deanRioClaroBrazilian1976, p. 56].

### Heading 3

Include equations like these:

$(1)$ $f(x)=x^2$

$(2)$ $k_{n+1} = n^2 + k_n^2 - k_{n-1}$

$(3)$ $\frac{\frac{1}{x}+\frac{1}{y}}{y-z}$

## References
```

####  Utilizando pandoc para conversão do arquivo Markdown

O próximo passo é converter o arquivo paper1.md para pdf ou odt/docx. O código do pandoc é simples (```pandoc test.md -o test.pdf```), sendo executado no terminal de seu computador (geralmente após o símbolo $).

Para adicionar as citações bibliográficas e a bibliografia final é preciso incluir ainda ```--citeproc``` e ```--bibliography```, seguidos do arquivo .bib utilizado. Alternativamente, o elemento ```--bibliography``` pode ser incluído nos metadados da seção YAML (```bibliography: biblio.bib```). Neste tutorial usaremos ```--bibliography``` no comando de linha. Para os detalhes, consultar a documentação do pandoc para [criação de pdf](https://pandoc.org/MANUAL.html#creating-a-pdf) e [outros formatos](https://pandoc.org/MANUAL.html#general-options). Como ilustração, a sequência seguinte converte o arquivo paper1.md para pdf e docx:

- No terminal de seu computador, use $ cd ... para ir ao diretório "artigo", onde o arquivo paper1.md e biblio.bib foram salvos.

- Copie e cole no terminal: 

  $ pandoc paper1.md --citeproc --bibliography biblio.bib -o paper1.pdf

- Verifique o novo arquivo paper.pdf no diretório. A formatação do documento e das referências é feita automaticamente pelo pandoc em um típico documento LaTeX.

- Para odt ou docx, apenas altere o output, de pdf para odt/docx: 

  $ pandoc paper1.md --citeproc --bibliography biblio.bib -o paper1.docx

- Verifique o arquivo paper1.pdf no seu diretório "artigo". Caso as instalações dos programas necessários estiverem em ordem, o arquivo em pdf terá a estrutura do Markdown copiado e colado na seção anterior, tal como o que se encontra na pasta "exemplos" deste tutorial no GitHub (ver paper1.pdf).

- É mais prático manter o arquivo .bib (aqui, biblio.bib) em uma pasta separada dentro do diretório "artigo" que contém o arquivo Markdown. Para isso, crie uma nova pasta (p.ex. com o nome ref) dentro do diretório "artigo" e transfira biblio.bib para ela. O código no terminal agora deve incluir uma barra após ref (isto é, ref/): 

  $ pandoc paper1.md --citeproc --bibliography ref/biblio.bib -o paper1.pdf 

- Como exemplo adicional, copie o texto abaixo (inclusive ```---``` no início e no final do arquivo YAML) e cole em um arquivo em branco do Typora ou outro editor Markdown (lembrando: para copiar, passe o cursor no texto abaixo e clique no símbolo no alto à direita). Salve este arquivo no mesmo diretório "artigo" como paper2.md:

```markdown
---
title: Latifundia and Land Policy in Nineteenth-Century Brazil
author: Warren Dean 
date: 1 November 1971
---

[This is an extract from the original article]

Anyone who claimed to have the means and desire to make use of the land was given a grant, customarily one to three leagues in extent (16.7 to 50.1 square miles). The royal grants, called sesmarias, were clearly not homesteads; a labor force would have to be introduced to carry out the manual labor. This was difficult for Portugal to provide. Anyone with the necessary 300 to 400 milreis (375 to 500 U.S. dollars of i8oo) to pay for the formalities could obtain a sesmaria. Any immigrant who lacked that amount could squat on unclaimed crown lands. This was illegal, and therefore precarious, but it was seldom punished or even noticed unless another person later acquired a grant over the squatter's land. Some Portuguese did remain on the sesmarias of others as tenants of a sort, but because they had the alternative of squatting, the landowner could not demand much steady labor from them. Hence the introduction of slave labor, first Indian, then African. The latifundium, slavery, and the export trade remained, as the historian, Caio Prado, Jr. has said, for more than three hundred years the principal institutions of Brazilian society.[^1]

[^1]: Evsey Domar has made a theoretical statement of the origins of slave labor: given a leisured elite, there cannot exist simultaneously cheap land andf ree labor. If either of these elements is eliminated, free labor is possible.[@domarCausesSlaverySerfdom1970]

## References
```

- Copie e cole no seu terminal o código abaixo para gerar o novo pdf e depois verifique o resultado na pasta "artigo":

  $ pandoc paper2.md --citeproc --bibliography ref/biblio.bib -o paper2.pdf 

#### Definindo estilos de citação de periódicos

Além do default do pandoc, outros estilos de citação podem ser definidos facilmente utilizando o repositório de CSL (Citation Style Language) do Zotero. Vários periódicos possuem CSL pronto para ser utilizado, como pode ser visto em https://www.zotero.org/styles.

- Faça o download neste site (https://www.zotero.org/styles) do arquivo .csl desejado e salve na pasta ref, ao lado do arquivo biblio.bib. Nos exemplos a seguir, serão utilizados os estilos de duas revistas, Explorations in Economic History e Hispanic American Historical Review. Os dois arquivos .csl também estão disponíveis na pasta "csl" nesta página do GitHub.

- No terminal, complemente o código anterior com ```--csl ref/[...].csl```, onde [...] é o nome/CSL do periódico. Utilizando o arquivo paper2 execute os dois códigos, alternadamente:

  $ pandoc paper2.md --citeproc --bibliography ref/biblio.bib --csl ref/hispanic-american-historical-review.csl  -o paper2_hahr.pdf

  $ pandoc paper2.md --citeproc --bibliography ref/biblio.bib --csl ref/explorations-in-economic-history.csl  -o paper2_eeh.pdf

- Verifique os resultados no diretório. 

#### Configuração dos metadados YAML

O bloco com metadados YAML que é inserido no início do documento Markdown contempla os itens principais do "heading" de um artigo acadêmico, como título, autor, data, resumo e palavras-chave. Ver as opções na [documentação do pandoc](https://pandoc.org/MANUAL.html#variables). 

- Para inserir duas linhas após uma entrada no bloco YAML, usar ```|``` duas vezes:

```yaml
author: |
   | name
   | institution
```

- O exemplo abaixo acrescenta outras informações do autor e inclui mais itens dos metadados do bloco YAML (```thanks``` e ```abstract```):

```yaml
---
title: Latifundia and Land Policy in Nineteenth-Century Brazil
author: |
  | Warren Dean
  | University of New York
  | address
date: 1 November 1971
thanks: "I thank to..."
abstract: "This paper examines..."
---
```

- Copie o bloco YAML acima em paper2.md e veja o resultado após executar no comando de linha:

  $ pandoc paper2.md --citeproc --bibliography ref/biblio.bib --csl ref/hispanic-american-historical-review.csl  -o paper2.pdf

#### Inserindo figuras no artigo

Com Markdown, figura e título são editados de maneira simples, com o seguinte formato:

```markdown
![title](file.png)
```

Pode-se também diferenciar tamanho e tipo de fontes, bem como adicionar Fontes e Notas abaixo do título, como é comum em artigos acadêmicos. Para ilustrar, criaremos um outro arquivo para a edição de figuras. 

- Copie o texto abaixo (inclusive ```---``` no início e no final do bloco YAML) e cole em um arquivo em branco do Typora ou outro editor Markdown (novamente: para copiar, passe o cursor no texto abaixo e clique no símbolo no alto à direita). Salve este arquivo no mesmo diretório "artigo" como paper3.md:

```markdown
---
title: The Colonial Nucleus of Barão de Antonina, São Paulo
author: |
  | Pierre Monbeig
  | University of São Paulo
  | @address
date: 1 April 1940
thanks: "I thank to..."
abstract: "This article examines..."
---

[These are parts of the original article]

The wave of immigration that invaded Brazil in the last decades of the nineteenth century contributed to the peopling of the southern states in distinctly different ways. In Paraná, Santa Catharina, and Rio Grande do Sul the new arrivals effected a true settlement of the country, in small, economically viable holdings. In São Paulo, on the other hand, the immigrants served mainly as laborers for the coffee fazendeiros; many of them were small Italian farmers who had exchanged for a lot unenviable enough, but in which they at least had their liberty, the position of agricultural proletariat in an environment often geographically and psychologically unfavorable. Before long, however, the state of São Paulo undertook the establishment of "centers of colonization." Nova Odessa and Nova Europa are the best known of these official nucleus of settlement.[^1] This method of settlement has been sustained by the state government, and there are now several nucleos, administered by the Department of Lands, Colonization, and Immigration of the Secretariat of Agriculture. Three are in the littoral zone to the south of Santos: Itanhaém on the shore, Alecrim at the foot of the Serra do Mar, and Juquiá on the densely forested slopes. Another "nucleus" in the early stages is on the plateau at Sao Miguel; but the most important is in the interior -- the "núcleo colonial Barão de Antonina." Not only does Barão de Antonina afford a good example of the modern ways of life in the state of São Paulo; it is also a concrete expression of the Brazilian policy of colonization.

(...)

The ethnic composition of the government colonies (see p. 260) varies according to geographical situation and age. In Itanhaém, Brazilians own 56.7 percent of the land, and Portuguese and Spaniards, the most important foreign element, own 13.9 and I2.8 per cent respectively. In this low, humid area, where the banana is the staple crop, other immigrants have not adapted themselves to its cultivation. On the other hand, the site of Alecrim is favorable for rice and vegetables, and Japanese own 34.5 per cent of the area, Brazilians 5I.9 per cent, and Portuguese, far behind in third place, only 6.2 per cent. In Juquiá, Brazilian colonists occupy 91.3 per cent of the land -- understandably enough, for the colony is in the dense forest and it is the Brazilian who is the true pioneer. Only afterwards comes the foreigner. In the young "nucleus" of São Miguel, where campos are interspersed in the forest, the first colonists are indifferently Brazilians or foreigners. In the case of Barão de Antonina, as has been said, clearing was effected by the caboclos.

What is the attitude toward one another of elements so diverse? To what degree do they mix with one another and with the Brazilians? The normal play of affinities tends to unite the colonists of the same origin. The Lithuanians gather in the evenings to sing and dance at the home of one of their group. Also, normally the most advanced member of any group tends to play the part of moral and financial adviser; for instance, the Rumanians, almost all Bessarabians, are under the leadership of a former officer. This does not make for disharmony but tends to ease the process of acclimatization. Contacts with the Brazilian element are frequent enough, especially by means of the school. In most of the houses one finds foreign-language papers, especially Polish or German, almost exclusively agricultural, not political, in character. The children in the rural school, whatever their color and the nationality of their parents, become the educators of the parents, introducing into the home books and magazines in the Portuguese language. The shops of the sede facilitate the establishment of relations; so does the farm work. The organizers of the colony have shown themselves wise in the drawing up of plans: lots have been distributed so that the creation of ethnic islands is impossible. Brazilians and foreigners are mingled, and the foreigners themselves are mingled so far as possible. Some Japanese settled before 1930 remain grouped; but mingling with the other elements is more advanced than it is among Japanese farmers in the pioneer zones proper. Nearness makes for contacts, especially for new arrivals to the neighborhood who need aid in tools and labor for building their houses and clearing their land.

![Ilustrations of the mixture of nationalities at Barão de Antonina.](fig_monbeig1.png)

(...)

One of the surest means of rooting is the prosperity of the small farmer. If the economic situation of the foreign colonists is compared with that of the Brazilian, the foreigners will be found to have acquired a small capital within a few years whereas the Brazilians are far from it. The files of the colonization services afford excellent documentation; they permit one to trace the fortunes of individual colonists. A Japanese who had emigrated to Brazil in I9I9 and worked in fazendas until 1930 arrived at the colony without money and in debt and obtained a 78-hectare holding at a price of 90 mil-réis a hectare, payable in ten years: he now has I9 hectares under cultivation-sugar cane, cotton, coffee, maize, oranges, bananas, barley, soybeans, Brazilian beans (feijão), rice, and garlic-and a small cane-liquor still; he owns 12 horses, 20 sheep and goats, 46 pigs, 50 hens, and 70 hives of bees; and his property is valued at 30 contos. A Russian colonist, Romanoff by name, who left China in 193I and arrived with 3 contos bought 90 hectares: 36 are now cleared; besides crops as varied as those of the Japanese he has a sawmill and a truck and the finest house in the colony, with a radio and a small electric plant; and his property is valued at 100 contos, of which 76 are in buildings, equipment, and the like. 

![Wheat harvest in Barão de Antonina](fig_monbeig2.png)

A Lithuanian acquired 26 hectares in 1931 with an outlay of 200 mil-réis, with which he bought also a horse and two pigs: now half his land is in wheat, barley, oats, rye, rice, cotton, beans, manioc, potatoes, maize, and vegetables; he produces and sells eggs, milk, butter, and honey; his house is well furnished and is surrounded with a flower garden, and near by are a reservoir and a plow shed; his stock comprises 2 cows, 3 mules, and 40 head of poultry; and his property is valued at 30 contos. Two Brazilians arrived in 1932 with meager resources; one took 29 hectares, the other 48: they work 12 and I5 hectares respectively, in rice, cotton, beans, manioc, and maize; their stock is comparable with that of the foreigners (2 pigs, 4 cows, and 3 horses; 48 pigs, 2 horses, 150 poultry, and 3 cows); but their properties show few improvements and are valued at no more than 16 and 10 contos respectively. A visit to the colony confirms the evidence of the archives: in general the houses of the foreigners are more up-to-date and more comfortable than those of the Brazilian colonists; the goods and chattels of the colonists who carry the weight of the caboclo.



[^1]: Pierre Denis's classic work "Le Bresil au XXe siecle" [@denisBresilAuXX1909] gives an excellentd escription of these centers in about I908.

## References
```

- Note que no meio do texto de paper3.md há duas figuras (fig_monbeig1.png e fig_monbeig2.png) com seus respectivos títulos, conforme a formatação em Markdown citada acima:

  ```markdown
  ![Ilustrations of the mixture of nationalities at Barão de Antonina.](fig_monbeig1.png)
  
  ![Wheat harvest in Barão de Antonina](fig_monbeig2.png)
  ```

- Baixe as duas figuras disponíveis na pasta "figuras" deste tutorial no GitHub e salve na sua pasta "artigo", como nas vezes anteriores. Copie o cole o código abaixo no terminal e confira o resultado:

  $ pandoc paper3.md --citeproc --bibliography ref/biblio.bib --csl ref/hispanic-american-historical-review.csl  -o paper3.pdf

- Se foram salvas corretamente no diretório, ambas figuras estarão numeradas como Figure 1 e Figure 2 no novo pdf. O pandoc gera a numeração das figuras automaticamente, na ordem em que estiverem dispostas no artigo. 

- Além do título, uma figura requer geralmente a citação de suas fontes, a inclusão de notas explicativas e diferenciação na formatação do texto. Aqui aparecem as primeiras combinações de Markdown com a sintaxe do LaTeX (mais sobre esse recurso adiante).

- A título de exemplo, os seguintes comandos do LaTeX são incluídos no primeiro exemplo: ```\newline``` é inserido em ```[title]``` para quebrar a linha a fim de incluir "Sources"; ```\small``` diferencia o tamanho da fonte e ```\textit{ }``` adiciona itálico em "Note".


```markdown
![title \newline \small \textit{Note:} note's text.](file.png)
```

- Na Figure 1 do arquivo paper3.md, adicione o seguinte texto em "Note": "Key: i, Brazilian; 2, Austrian; 3, German; 4, Estonian; 5, Czechoslovakian; 6, Italian; 7, Russian; 8, Hungarian; 9, Lithuanian; 10, Japanese; 11, unsold lot." 
- Inclua também ```\newline```, ```\small``` e ```\textit { }``` conforme a estrutura acima. Assim:

```markdown
![Ilustrations of the mixture of nationalities at Barão de Antonina. \newline \small \textit{Note:} Key: 1, Brazilian; 2, Austrian; 3, German; 4, Estonian; 5, Czechoslovakian; 6, Italian; 7, Russian; 8, Hungarian; 9, Lithuanian; 10, Japanese; 11, unsold lot.](fig_monbeig1.png)
```

- Após a inclusão desta nova formatação de Figure 1, execute o mesmo código anterior do pandoc no terminal e veja o resultado no pdf:

  $ pandoc paper3.md --citeproc --bibliography ref/biblio.bib --csl ref/the-economic-history-review.csl  -o paper3.pdf

- Pela mesma lógica, pode-se incluir uma nova linha com a fonte da figura. No exemplo, acrescente-a logo após o título principal de Figure 1: ```\newline \small \textit{Source:} Monbeig, "Colonial Nucleus," p. 268```. Também é possível configurar o tamanho da figura  com ```{width=xx%}```, conforme abaixo:

  ```markdown
  ![Ilustrations of the mixture of nationalities at Barão de Antonina. \newline \small \textit{Source:} Monbeig, "Colonial Nucleus," p. 268. \newline \small \textit{Note:} Key: i, Brazilian; 2, Austrian; 3, German; 4, Estonian; 5, Czechoslovakian; 6, Italian; 7, Russian; 8, Hungarian; 9, Lithuanian; 10, Japanese; II, unsold lot.](fig_monbeig1.png){width=80%}
  ```

- Se preferir, copie e cole o bloco acima no paper3.md, execute pandoc no terminal e verifique o resultado no seu diretório "artigo":

  $ pandoc paper3.md --citeproc --bibliography ref/biblio.bib --csl ref/hispanic-american-historical-review.csl  -o paper3.pdf

#### Formatando tabelas

- O texto básico em Markdown pode ser integrado com a rica sintaxe do LaTeX para a edição de tabelas, de acordo com os padrões de uma publicação acadêmica. 

- Vamos criar outro arquivo para o exemplo com tabelas. Copie o texto abaixo (inclusive ```---``` no início e no final do bloco YAML) e cole em uma página em branco do Typora ou outro editor Markdown (novamente: passe o cursor no texto abaixo e clique no símbolo no alto à direita para copiar). Salve este arquivo como paper4.md no mesmo diretório "artigo" de antes.

  ```markdown
  ---
  title: Neither Slave nor Free. The Emancipados of Brazil, 1818-1868
  author: |
    | Robert Conrad
    | University of Illinois
    | email address
  date: 1 February 1973
  thanks: "I thank to..."
  abstract: "This article examines..."
  ---
  
  [Paragraphs of the original article]
  
  Exact statistics on emancipados are not available, but fragmentary information does exist. In 1865, after years of British insistence that information on free Africans be collected, the Brazilian government searched its archives and came up with statistics on 8,673 persons (see Tables I and II). Of these, 1,684 were recorded as dead, 1,890 were known to have received their secondary and final letters of emancipation, and 5,099 were thought to be still in bondage. Of the latter group, however, only 2,565 could be accounted for at that date, and the fate of the remaining 2,534 was unknown. Referring to the latter group, the British Consul at Rio wrote to the Foreign Office in 1865: "The remainder it is suggested have been stolen, have died and no return has been made of their deaths, and some few may have received certificates of emancipation."
  
  [Insert table here]
  
  Many, of course, were excluded from the record. An unknown number freed in northern provinces were missing from the list, including all those freed during the last years of the illegal slave trade in Pernambuco and in other northern provinces. Missing were 142 Africans landed in the northern province of Maranhão in 1826 from the schooner Carolina and there partially absorbed into the slave population. Completely forgotten were 518 Africans of a cargo of 1,000 seized after landing at Santos in i851, 18i captured at Serinhaem in Pernambuco in 1856, and another 313 brought to Brazil on the yacht Mary E. Smith in 1856.Most emancipados leased to private persons were employed, like most slaves in Brazil, in agriculture or domestic service. In cities, however, they were sometimes used as pretos de ganho, hiring themselves to the public and giving a set amount to their masters. Many women were rented as wet nurses, their own children reportedly being either left to foundling homes or illegally baptized as slaves.12 Africans kept under the direct control of the government were used mainly in urban occupations. In 1821 freedmen from the schooner Emília (see Table I) were assigned to the illumination of Rio's streets, to the police station, and to the water works, and three married couples were singled out for the upkeep of the Passeio Público, a fashionable square. Thirty years later (in 1851) freedmen could be found serving in the Misericordia Hospital, in powder and iron factories, in leper houses, in the Colegio Pedro II, the National Museum and other public places. Some worked in convents of the various religious orders, and others continued to light the city streets.
  
  (...)
  ```
  
- Copie e insira a seguinte tabela em LaTeX após o primeiro parágrafo, no lugar definido por "[Insert table here]":

```latex
  \begin{table}[!h]
  \centering\
  \caption{Africans freed by Mixed Commission, 1818-1845}
  \begin{tabular}{cccc}
  \hline\hline
   Date   & Type of Ship   & Name of Ship       &   Emancipados \\
  \hline
   1821   & Schooner       & Emília             &           352 \\
   1830   & Brig           & Oriental           &            56 \\
   1830   & Bark           & Eliza              &            50 \\
   1830   & -            & Estevão de Athaide &            50 \\
   1831   & Schooner       & Destemida          &            50 \\
   1834   & -            & Duque de Braganza  &           249 \\
   1834   & Pinnace        & Santo Antonio      &            91 \\
   1835   & Brigantine     & Rio da Prata       &           240 \\
   1835   & Smack          & Continente         &            60 \\
   Total  &             &                 &          1198 \\
  \hline
  \multicolumn{4}{l}{\textit{Source:} FO 84/1244, PRO.}\\
  \end{tabular}
  \end{table}
```

- Esta é uma típica tabela com a sintaxe do LaTeX. O texto Markdown com a tabela ficará assim:

  ```markdown
  ---
    title: Neither Slave nor Free. The Emancipados of Brazil, 1818-1868
    author: |
      | Robert Conrad
      | University of Illinois
      | email address
    date: 1 February 1973
    thanks: "I thank to..."
    abstract: "This article examines..."
    ---
    
    [Paragraphs of the original article]
    
  Exact statistics on emancipados are not available, but fragmentary information does exist. In 1865, after years of British insistence that information on free Africans be collected, the Brazilian government searched its archives and came up with statistics on 8,673 persons (see Tables I and II). Of these, 1,684 were recorded as dead, 1,890 were known to have received their secondary and final letters of emancipation, and 5,099 were thought to be still in bondage. Of the latter group, however, only 2,565 could be accounted for at that date, and the fate of the remaining 2,534 was unknown. Referring to the latter group, the British Consul at Rio wrote to the Foreign Office in 1865: "The remainder it is suggested have been stolen, have died and no return has been made of their deaths, and some few may have received certificates of emancipation."
    
  \begin{table}[!h]
  \centering\
  \caption{Africans freed by Mixed Commission, 1818-1845}
  \begin{tabular}{cccc}
  \hline\hline
   Date   & Type of Ship   & Name of Ship       &   Emancipados \\
  \hline
   1821   & Schooner       & Emília             &           352 \\
   1830   & Brig           & Oriental           &            56 \\
   1830   & Bark           & Eliza              &            50 \\
   1830   & -            & Estevão de Athaide &            50 \\
   1831   & Schooner       & Destemida          &            50 \\
   1834   & -            & Duque de Braganza  &           249 \\
   1834   & Pinnace        & Santo Antonio      &            91 \\
   1835   & Brigantine     & Rio da Prata       &           240 \\
   1835   & Smack          & Continente         &            60 \\
   Total  &             &                 &          1198 \\
  \hline
  \multicolumn{4}{l}{\textit{Source:} FO 84/1244, PRO.}\\
  \end{tabular}
  \end{table}
    
  Many, of course, were excluded from the record. An unknown number freed in northern provinces were missing from the list, including all those freed during the last years of the illegal slave trade in Pernambuco and in other northern provinces. Missing were 142 Africans landed in the northern province of Maranhão in 1826 from the schooner Carolina and there partially absorbed into the slave population. Completely forgotten were 518 Africans of a cargo of 1,000 seized after landing at Santos in i851, 18i captured at Serinhaem in Pernambuco in 1856, and another 313 brought to Brazil on the yacht Mary E. Smith in 1856.Most emancipados leased to private persons were employed, like most slaves in Brazil, in agriculture or domestic service. In cities, however, they were sometimes used as pretos de ganho, hiring themselves to the public and giving a set amount to their masters. Many women were rented as wet nurses, their own children reportedly being either left to foundling homes or illegally baptized as slaves.12 Africans kept under the direct control of the government were used mainly in urban occupations. In 1821 freedmen from the schooner Emília (see Table I) were assigned to the illumination of Rio's streets, to the police station, and to the water works, and three married couples were singled out for the upkeep of the Passeio Público, a fashionable square. Thirty years later (in 1851) freedmen could be found serving in the Misericordia Hospital, in powder and iron factories, in leper houses, in the Colegio Pedro II, the National Museum and other public places. Some worked in convents of the various religious orders, and others continued to light the city streets.
    
    (...)
  ```

- No terminal, execute o código do pandoc com o arquivo paper4.md e veja o resultado:

  $ pandoc paper4.md --citeproc --bibliography ref/biblio.bib --csl ref/hispanic-american-historical-review.csl  -o paper4.pdf

- Note que o pandoc incorpora o ambiente ```tabular```, que é o default do LaTeX para a criação de tabelas. Observe também que ```multicolumn{4}{l}{\textit{Source:} FO 84/1244, PRO.}``` é suficiente para criar o campo da Fonte no rodapé da tabela. 

- Além de ```tabular``` como default, outros pacotes de tabelas do LaTeX, como ```tabulary``` e ```tabularx```, são compatíveis com Markdown e pandoc. Para tanto, basta adicionar o ambiente ```header-includes: |``` aos metadados do YAML do documento Markdown, acompanhado de ```\usepackage{ }``` para cada um dos pacotes, tal como no preâmbulo do LaTeX. 

- Por exemplo, no caso de ```tabularx``` e ```tabulary``` o cabeçalho YAML é editado desta forma:

```yaml
---
title: Neither Slave nor Free. The Emancipados of Brazil, 1818-1868
author: |
  | Robert Conrad
  | University of Illinois
  | email address
date: 1 February 1973
thanks: "I thank to..."
abstract: "This article examines..."

header-includes: |
	\usepackage{tabularx}
	\usepackage{tabulary}
---
```

- Copie e cole ```header-includes: |``` e os pacotes na seção do YAML e substitua a tabela anterior com a formatada com ```tabulary ``` no arquivo paper4.md, como indicado abaixo (ou simplesmente copie e cole todo o texto):

```markdown
---
  title: Neither Slave nor Free. The Emancipados of Brazil, 1818-1868
  author: |
    | Robert Conrad
    | University of Illinois
    | email address
  date: 1 February 1973
  thanks: "I thank to..."
  abstract: "This article examines..."
  
  header-includes: |
	\usepackage{tabularx}
	\usepackage{tabulary}
---
  
  [Paragraphs of the original article]
  
Exact statistics on emancipados are not available, but fragmentary information does exist. In 1865, after years of British insistence that information on free Africans be collected, the Brazilian government searched its archives and came up with statistics on 8,673 persons (see Tables I and II). Of these, 1,684 were recorded as dead, 1,890 were known to have received their secondary and final letters of emancipation, and 5,099 were thought to be still in bondage. Of the latter group, however, only 2,565 could be accounted for at that date, and the fate of the remaining 2,534 was unknown. Referring to the latter group, the British Consul at Rio wrote to the Foreign Office in 1865: "The remainder it is suggested have been stolen, have died and no return has been made of their deaths, and some few may have received certificates of emancipation."
  
\begin{table}[!h]
\centering\
\caption{Africans freed by Mixed Commission, 1818-1845}
\begin{tabulary}{\linewidth}{cccc}
\hline\hline
 Date   & Type of Ship   & Name of Ship       &   Emancipados \\
\hline
 1821   & Schooner       & Emília             &           352 \\
 1830   & Brig           & Oriental           &            56 \\
 1830   & Bark           & Eliza              &            50 \\
 1830   & -            & Estevão de Athaide &            50 \\
 1831   & Schooner       & Destemida          &            50 \\
 1834   & -            & Duque de Braganza  &           249 \\
 1834   & Pinnace        & Santo Antonio      &            91 \\
 1835   & Brigantine     & Rio da Prata       &           240 \\
 1835   & Smack          & Continente         &            60 \\
 Total  &             &                 &          1198 \\
\hline
\multicolumn{4}{l}{\textit{Source:} FO 84/1244, PRO.}\\
\end{tabulary}
\end{table}
  
Many, of course, were excluded from the record. An unknown number freed in northern provinces were missing from the list, including all those freed during the last years of the illegal slave trade in Pernambuco and in other northern provinces. Missing were 142 Africans landed in the northern province of Maranhão in 1826 from the schooner Carolina and there partially absorbed into the slave population. Completely forgotten were 518 Africans of a cargo of 1,000 seized after landing at Santos in i851, 18i captured at Serinhaem in Pernambuco in 1856, and another 313 brought to Brazil on the yacht Mary E. Smith in 1856.Most emancipados leased to private persons were employed, like most slaves in Brazil, in agriculture or domestic service. In cities, however, they were sometimes used as pretos de ganho, hiring themselves to the public and giving a set amount to their masters. Many women were rented as wet nurses, their own children reportedly being either left to foundling homes or illegally baptized as slaves.12 Africans kept under the direct control of the government were used mainly in urban occupations. In 1821 freedmen from the schooner Emília (see Table I) were assigned to the illumination of Rio streets, to the police station, and to the water works, and three married couples were singled out for the upkeep of the Passeio Público, a fashionable square. Thirty years later (in 1851) freedmen could be found serving in the Misericordia Hospital, in powder and iron factories, in leper houses, in the Colegio Pedro II, the National Museum and other public places. Some worked in convents of the various religious orders, and others continued to light the city streets.
  
  (...) 
```

- Gere o pdf com pandoc no terminal e confira o resultado:

$ pandoc paper4.md --citeproc --bibliography ref/biblio.bib --csl ref/hispanic-american-historical-review.csl -o paper4.pdf

#### Outros elementos dos metadados

- Os metadados da seção YAML admitem outras opções para a formatação final do documento em LaTeX, tais como ```documentclass```, ```papersize``` e ```geometry```. Ver abaixo:
```markdown
---
title: Neither Slave nor Free. The Emancipados of Brazil, 1818-1868
author: |
  | Robert Conrad
  | University of Illinois
  | email address
date: 1 February 1973
thanks: "I thank to..."
abstract: "This article examines..."
documentclass: article
papersize: a4
geometry:
- top=30mm
- left=25mm
- right=25mm

header-includes: |
	\usepackage{tabularx}
	\usepackage{tabulary}
---

 [Paragraphs of the original article]
  
Exact statistics on emancipados are not available, but fragmentary information does exist. In 1865, after years of British insistence that information on free Africans be collected, the Brazilian government searched its archives and came up with statistics on 8,673 persons (see Tables I and II). Of these, 1,684 were recorded as dead, 1,890 were known to have received their secondary and final letters of emancipation, and 5,099 were thought to be still in bondage. Of the latter group, however, only 2,565 could be accounted for at that date, and the fate of the remaining 2,534 was unknown. Referring to the latter group, the British Consul at Rio wrote to the Foreign Office in 1865: "The remainder it is suggested have been stolen, have died and no return has been made of their deaths, and some few may have received certificates of emancipation."
  
\begin{table}[!h]
\centering\
\caption{Africans freed by Mixed Commission, 1818-1845}
\begin{tabulary}{\linewidth}{cccc}
\hline\hline
 Date   & Type of Ship   & Name of Ship       &   Emancipados \\
\hline
 1821   & Schooner       & Emília             &           352 \\
 1830   & Brig           & Oriental           &            56 \\
 1830   & Bark           & Eliza              &            50 \\
 1830   & -            & Estevão de Athaide &            50 \\
 1831   & Schooner       & Destemida          &            50 \\
 1834   & -            & Duque de Braganza  &           249 \\
 1834   & Pinnace        & Santo Antonio      &            91 \\
 1835   & Brigantine     & Rio da Prata       &           240 \\
 1835   & Smack          & Continente         &            60 \\
 Total  &             &                 &          1198 \\
\hline
\multicolumn{4}{l}{\textit{Source:} FO 84/1244, PRO.}\\
\end{tabulary}
\end{table}
  
Many, of course, were excluded from the record. An unknown number freed in northern provinces were missing from the list, including all those freed during the last years of the illegal slave trade in Pernambuco and in other northern provinces. Missing were 142 Africans landed in the northern province of Maranhão in 1826 from the schooner Carolina and there partially absorbed into the slave population. Completely forgotten were 518 Africans of a cargo of 1,000 seized after landing at Santos in i851, 18i captured at Serinhaem in Pernambuco in 1856, and another 313 brought to Brazil on the yacht Mary E. Smith in 1856.Most emancipados leased to private persons were employed, like most slaves in Brazil, in agriculture or domestic service. In cities, however, they were sometimes used as pretos de ganho, hiring themselves to the public and giving a set amount to their masters. Many women were rented as wet nurses, their own children reportedly being either left to foundling homes or illegally baptized as slaves.12 Africans kept under the direct control of the government were used mainly in urban occupations. In 1821 freedmen from the schooner Emília (see Table I) were assigned to the illumination of Rio's streets, to the police station, and to the water works, and three married couples were singled out for the upkeep of the Passeio Público, a fashionable square. Thirty years later (in 1851) freedmen could be found serving in the Misericordia Hospital, in powder and iron factories, in leper houses, in the Colegio Pedro II, the National Museum and other public places. Some worked in convents of the various religious orders, and others continued to light the city streets.
  
  (...) 
```

- Copie e cole os valores de ```documentclass```, ```papersize``` e ```geometry``` em paper4.md. Veja o resultado copiando e executando o código no terminal:

​     $ pandoc paper4.md --citeproc --bibliography ref/biblio.bib --csl ref/the-economic-history-review.csl  -o paper4.pdf

#### Formatação final e exemplo

- Outras bibliotecas do LaTeX compatíveis com Pandoc podem ser adicionadas ao ```header-includes: |``` no bloco YAML para a formatação final do artigo, de acordo com as opções de formatação desejadas ou recomendadas por um periódico.
- O exemplo abaixo reproduz os metadados de um working paper, "[Predicting Skills of Runaway Slaves in São Paulo, 1854-1887](http://www.repec.eae.fea.usp.br/documentos/Colistete_15WP.pdf)" (Departamento de Economia, FEA-USP, WP no. 2021-15, 2021). O resultado final da edição com Markdown, pandoc, LaTeX e Zotero pode ser [conferido aqui](http://www.repec.eae.fea.usp.br/documentos/Colistete_15WP.pdf).
```latex
title: Predicting Skills of Runaway Slaves in São Paulo, 1854-1887
author: |
  | Renato P. Colistete
  | University of São Paulo
  | rcolistete@usp.br
date: 15 April 2021
abstract: "This paper examines the skills of enslaved labour during the second half of the nineteenth century in the province of São Paulo. The analysis is based on data from 3,376 individuals collected in advertisements of runaway slaves published by São Paulo newspapers between 1854 and 1887. As only a small part of the announcements listed runaways' occupations, we draw on individual details on sex, age, ethnicity, residence, physical characteristics and other features of fugitives with advertised occupations to predict the skills of the remaining subset of runaways, using classification algorithms from machine learning. Overall, both observed and predicted skilled runaways converged in their characteristics: skilled runaways were mostly male, older than their low-skilled counterparts and predominantly from farms and plantations, rather than urban settings. Africans were not at a disadvantage in artisanal jobs when compared with Brazilian-born runaways, and the skill gap between mixed-race and black fugitives was negligible. Although the enslaved population suffered from very low levels of literacy, the few runaways with an ability to read or write tended to work in more qualified and artisanal occupations, indicating that education may have been valuable even under the appalling conditions of slavery. These results are important both for the analysis of slavery in Brazil and comparisons with other plantation societies in the Americas."
bibliography: bib_ref.bib
documentclass: article
papersize: a4
geometry:
- top=30mm
- left=25mm
- right=25mm

header-includes: |
    \usepackage{fancyhdr}
    \pagestyle{fancy}
    \fancyhead[R]{}
    \usepackage{sectsty}
    \sectionfont{\clearpage}
    \sectionfont{\centering}
	\usepackage{booktabs}
	\usepackage{tabularx}
	\usepackage{tabulary}
	\usepackage{makecell}
	\renewcommand\theadfont{\normalsize}
	\usepackage{caption}
	\captionsetup[table]{labelfont=bf, skip=3mm}
	\captionsetup[figure]{labelfont=bf, skip=3mm}
    \usepackage{subcaption}
    \usepackage{wrapfig} 
    \usepackage[sc,osf]{mathpazo}
    \usepackage{graphicx}
    \usepackage{xcolor}
    \usepackage{float}
	\floatplacement{figure}{h}
	\linespread{1.1}
    \usepackage[bottom,norule,hang]{footmisc}
    \setlength{\footnotemargin}{3mm}
    \setlength{\skip\footins}{3mm}
	\setlength{\footnotesep}{3mm}
```

#### Concluindo

Em resumo, o uso de Markdown combinado com Pandoc, Zotero e LaTeX é uma opção prática e consistente para edição de artigos e demais trabalhos acadêmicos, constituindo uma excelente alternativa tanto para quem usa Word na área de humanas quanto para os que utilizam LaTeX em editores como Overleaf. 
