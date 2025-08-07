# ANÁLISE Coleguium


**Thales Ribeiro Melo, thalesm1819@gmail.com**


---

_**Resumo**. Relatório da análise feita das matrículas das unidades do Colégio Coleguium. 

---


## Introdução

Esse trabalho teve como objetivo demonstrar minhas habilidades e potencial para conseguir a vaga de analista de dados. 


###    Objetivos gerais

Os objetivos dessa análise foi responder 3 questões:

1. Análise de tendências: identificação do tempo médio que as famílias levam para se
matricular após a realização da inscrição e o período do ciclo de matrículas em que
esse tempo médio entre inscrição e matrícula é mais curto.
2. Identifique se há alguma correlação entre os descontos concedidos, o período do
ciclo e o volume de matrículas no período.
3. Quais unidades apresentam maior concessão de descontos e qual o % médio de
descontos concedidos em cada unidade? Relacione essa informação de quantidade
de descontos com a relação de nº de leads e matrículas para essa unidade.

---

## Análise exploratórida dos dados


### Preparação dos dados


Para preparar os dados foi feita a mesclagem das bases;

<pre lang="markdown">Assistente = Inscritos.merge(Matricula, on = 'Código Candidato', how = 'left')</pre>


Exclusão de nulos;

<pre lang="markdown">Assistente = Assistente.dropna(subset = 'Data de Inscrição')
 Assistente = Assistente.dropna(subset = 'Data da matrícula')</pre>```
 

Exclusão de valores duplos;

<pre lang="markdown">Assistente = Assistente.drop_duplicates(subset= ['Código Candidato', 'Data de Inscrição', 'Série'])</pre>```


Formatação dos valores das datas;

<pre lang="markdown">Assistente['Data de Inscrição'] = pd.to_datetime(Assistente['Data de Inscrição'], format='mixed', dayfirst=True)
Assistente['Data de Inscrição'] = Assistente['Data de Inscrição'].dt.date
Assistente['Data de Inscrição'] = pd.to_datetime(Assistente['Data de Inscrição'], format='%d/%m/%Y', dayfirst=True)
Assistente['Data da matrícula'] = pd.to_datetime(Assistente['Data da matrícula'], format="%d/%m/%Y")</pre>

---

## Resultados da análise de dados

### Primeira Análise:


**Objetivo: identificação do tempo médio que as famílias levam para sematricular após a realização da inscrição e o período do ciclo de matrículas em queesse tempo médio entre inscrição e matrícula é mais curto.**

A primeira análise foi feita calculando a diferença dos dias entre a data da inscrição e a matrícula. Então foi realizado a separação das novas matrículas das rematrículas.

<pre lang="markdown">Assistente['Diferença'] = (Assistente['Data da matrícula'] - Assistente['Data de Inscrição']).dt.days</pre>

<pre lang="markdown">matriculaNova = Assistente.loc[Assistente['Tipo'] == 'Matrícula nova']
rematrícula = Assistente.loc[Assistente['Tipo'] == 'Rematrícula']</pre>

**Observação: Essa separação foi feita durante toda a análise.**

#### **Resultados**

 média de dias para fazer uma nova matrícula é de: 28 dias.

 A média de dias para fazer uma rematrícula é de: 84 dias.
 

### Segunda Análise:

**Objetivo: Identifique se há alguma correlação entre os descontos concedidos, o período do ciclo e o volume de matrículas no período.**

A segunda análise foi feita separando a base em meses, contando o número de matrículas e calculando a média deles.

<pre lang = "markdown">dataNovaMatrícula = {
    'Meses' : ['Agosto', 'Setembro', 'Outubro','Novembro', 'Dezembro', 'Janeiro', 'Fevereiro'],
    'Media de Descontos' : [round(AgostoNM['Bolsa'].mean()), round(SetembroNM['Bolsa'].mean()), round(OutubroNM['Bolsa'].mean()), round(NovembroNM['Bolsa'].mean()), round(DezembroNM['Bolsa'].mean()), round(JaneiroNM['Bolsa'].mean()), round(FevereiroNM['Bolsa'].mean())],
    'Número de matrículas' : [AgostoNM['Bolsa'].count(), SetembroNM['Bolsa'].count(), OutubroNM['Bolsa'].count(), NovembroNM['Bolsa'].count(), DezembroNM['Bolsa'].count(), JaneiroNM['Bolsa'].count(), FevereiroNM['Bolsa'].count()]
}

dataRematrícula = {
    'Meses' : ['Agosto', 'Setembro', 'Outubro','Novembro', 'Dezembro', 'Janeiro', 'Fevereiro'],
    'Media de Descontos' : [round(AgostoRM['Bolsa'].mean()), round(SetembroRM['Bolsa'].mean()), round(OutubroRM['Bolsa'].mean()), round(NovembroRM['Bolsa'].mean()), round(DezembroRM['Bolsa'].mean()), round(JaneiroRM['Bolsa'].mean()), round(FevereiroRM['Bolsa'].mean())],
    'Número de matrículas' : [AgostoRM['Bolsa'].count(), SetembroRM['Bolsa'].count(), OutubroRM['Bolsa'].count(), NovembroRM['Bolsa'].count(), DezembroRM['Bolsa'].count(), JaneiroRM['Bolsa'].count(), FevereiroRM['Bolsa'].count()]
}</pre>


#### Resultados







### Terceira Análise




## Resultados



### Resultados obtidos com o modelo 1.

Apresente aqui os resultados obtidos com a indução do modelo 1. 
Apresente uma matriz de confusão quando pertinente. Apresente as medidas de performance
apropriadas para o seu problema. 
Por exemplo, no caso de classificação: precisão, revocação, F-measure, acurácia.


### Resultados obtidos com o modelo 2.

Repita o passo anterior com os resultados do modelo 2.


## 8. Conclusão

Apresente aqui a conclusão do seu trabalho. Discussão dos resultados obtidos no trabalho, 
onde se verifica as observações pessoais de cada aluno.

Uma conclusão deve ter 3 partes:

   * Breve resumo do que foi desenvolvido
	 * Apresenação geral dos resultados obtidos com discussão das vantagens e desvantagens do sistema inteligente
	 * Limitações e possibilidades de melhoria


# REFERÊNCIAS

Por exemplo:

**[1]** - _ELMASRI, Ramez; NAVATHE, Sham. **Sistemas de banco de dados**. 7. ed. São Paulo: Pearson, c2019. E-book. ISBN 9788543025001._

**[2]** - _COPPIN, Ben. **Inteligência artificial**. Rio de Janeiro, RJ: LTC, c2010. E-book. ISBN 978-85-216-2936-8._

**[3]** - _CORMEN, Thomas H. et al. **Algoritmos: teoria e prática**. Rio de Janeiro, RJ: Elsevier, Campus, c2012. xvi, 926 p. ISBN 9788535236996._

**[4]** - _SUTHERLAND, Jeffrey Victor. **Scrum: a arte de fazer o dobro do trabalho na metade do tempo**. 2. ed. rev. São Paulo, SP: Leya, 2016. 236, [4] p. ISBN 9788544104514._

**[5]** - _RUSSELL, Stuart J.; NORVIG, Peter. **Inteligência artificial**. Rio de Janeiro: Elsevier, c2013. xxi, 988 p. ISBN 9788535237016._



# APÊNDICES

**Colocar link:**

Do código (armazenado no repositório);
