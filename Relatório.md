# ANÁLISE Coleguium


**Thales Ribeiro Melo, thalesm1819@gmail.com**


---

**Resumo**. Relatório da análise feita das matrículas das unidades do Colégio Coleguium. 

---


## Índice

- [Introdução](#introdução)

- [Objetivos Gerais](#objetivos-gerais)

- [Preparação dos dados](#preparação-dos-dados)

- [Primeira Análise](#primeira-análise)

- [Segunda Análise](#segunda-análise)

- [Terceira Análise](#terceira-análise)

- [Conclusão](#conclusão)


---

## Introdução

Esse trabalho teve como objetivo demonstrar minhas habilidades e potencial para conseguir a vaga de analista de dados. 

---


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


### Preparação dos dados


Para preparar os dados foi feita a mesclagem das bases;

<pre lang="Python">Assistente = Inscritos.merge(Matricula, on = 'Código Candidato', how = 'left')</pre>


Exclusão de nulos;

<pre lang="Python">Assistente = Assistente.dropna(subset = 'Data de Inscrição')
Assistente = Assistente.dropna(subset = 'Data da matrícula')</pre>
 

Exclusão de valores duplos;

<pre lang="Python">Assistente = Assistente.drop_duplicates(subset= ['Código Candidato', 'Data de Inscrição', 'Série'])</pre>


Formatação dos valores das datas;

<pre lang="Python">Assistente['Data de Inscrição'] = pd.to_datetime(Assistente['Data de Inscrição'], format='mixed', dayfirst=True)
Assistente['Data de Inscrição'] = Assistente['Data de Inscrição'].dt.date
Assistente['Data de Inscrição'] = pd.to_datetime(Assistente['Data de Inscrição'], format='%d/%m/%Y', dayfirst=True)
Assistente['Data da matrícula'] = pd.to_datetime(Assistente['Data da matrícula'], format="%d/%m/%Y")</pre>

---


### Primeira Análise:


[Código](https://github.com/ThalesMelo1/Coleguium-Entrevista/blob/main/Code/An%C3%A1lise_1.ipynb)



**Objetivo: identificação do tempo médio que as famílias levam para sematricular após a realização da inscrição e o período do ciclo de matrículas em queesse tempo médio entre inscrição e matrícula é mais curto.**


A primeira análise foi feita calculando a diferença dos dias entre a data da inscrição e a matrícula. Então foi realizado a separação das novas matrículas das rematrículas.

<pre lang="Python">Assistente['Diferença'] = (Assistente['Data da matrícula'] - Assistente['Data de Inscrição']).dt.days</pre>

<pre lang="Python">matriculaNova = Assistente.loc[Assistente['Tipo'] == 'Matrícula nova']
rematrícula = Assistente.loc[Assistente['Tipo'] == 'Rematrícula']</pre>


**Observação: Essa separação foi feita durante toda a análise.**


### **Resultados**

 A média de dias para fazer uma nova matrícula é de: 28 dias.

 A média de dias para fazer uma rematrícula é de: 84 dias.

 ---
 

### Segunda Análise:

[Código](https://github.com/ThalesMelo1/Coleguium-Entrevista/blob/main/Code/An%C3%A1lise_2.ipynb)


**Objetivo: Identifique se há alguma correlação entre os descontos concedidos, o período do ciclo e o volume de matrículas no período.**


A segunda análise foi feita separando a base em meses, contando o número de matrículas e calculando a média deles.

<pre lang = "Python">dataNovaMatrícula = {
    'Meses' : ['Agosto', 'Setembro', 'Outubro','Novembro', 'Dezembro', 'Janeiro', 'Fevereiro'],
    'Media de Descontos' : [round(AgostoNM['Bolsa'].mean()), round(SetembroNM['Bolsa'].mean()), round(OutubroNM['Bolsa'].mean()), round(NovembroNM['Bolsa'].mean()), round(DezembroNM['Bolsa'].mean()), round(JaneiroNM['Bolsa'].mean()), round(FevereiroNM['Bolsa'].mean())],
    'Número de matrículas' : [AgostoNM['Bolsa'].count(), SetembroNM['Bolsa'].count(), OutubroNM['Bolsa'].count(), NovembroNM['Bolsa'].count(), DezembroNM['Bolsa'].count(), JaneiroNM['Bolsa'].count(), FevereiroNM['Bolsa'].count()]
}

dataRematrícula = {
    'Meses' : ['Agosto', 'Setembro', 'Outubro','Novembro', 'Dezembro', 'Janeiro', 'Fevereiro'],
    'Media de Descontos' : [round(AgostoRM['Bolsa'].mean()), round(SetembroRM['Bolsa'].mean()), round(OutubroRM['Bolsa'].mean()), round(NovembroRM['Bolsa'].mean()), round(DezembroRM['Bolsa'].mean()), round(JaneiroRM['Bolsa'].mean()), round(FevereiroRM['Bolsa'].mean())],
    'Número de matrículas' : [AgostoRM['Bolsa'].count(), SetembroRM['Bolsa'].count(), OutubroRM['Bolsa'].count(), NovembroRM['Bolsa'].count(), DezembroRM['Bolsa'].count(), JaneiroRM['Bolsa'].count(), FevereiroRM['Bolsa'].count()]
}</pre>



### Resultados


<img width="839" height="376" alt="image" src="https://github.com/user-attachments/assets/917924d4-6ecd-44cc-867a-3fbe83b014b3" />




<img width="977" height="376" alt="image" src="https://github.com/user-attachments/assets/c25dcf3e-5aee-4517-89b9-95921d035d0c" />


Existe uma enorme diferença de quantidade entre as novas matrículas e as rematrículas.
O que é possível perceber para as novas matrículas é que os meses de outubro, dezembro e novembro são os que mais tem registro de matrícula. 
Já nas rematrículas, o mês com mais registros foi o de janeiro.


A média de descontos sobe linearmente pelos meses nas rematrículas, chegando ao seu pico de quase 70% em fevereiro.
Enquanto nas novas matrículas, o pico acontece nos meses de novembro e dezembro.


---


### Terceira Análise

[Código](https://github.com/ThalesMelo1/Coleguium-Entrevista/blob/main/Code/An%C3%A1lise_3.ipynb)


**Objetivo: Quais unidades apresentam maior concessão de descontos e qual o % médio de descontos concedidos em cada unidade? Relacione essa informação de quantidade de descontos com a relação de nº de leads e matrículas para essa unidade.**


A terceira análise foi feita pegando os nomes de cada unidade do Coleguium.

<pre lang="Python">Aescolas1 = set(novaMatrícula['Unidade'].unique()) 
escolas2 = set(rematrícula['Unidade'].unique())</pre>


Então foi demonstrado quais unidades dão mais desconto.

Para novas matrículas esse foi o resultado:
Carajás;
Conceição do Mato Dentro;
Alípio de Melo;
Mais Pampulha;
Ouro Preto;
Lagoa Santa;
Castelo;
Mais Cidade Nova;
Carlos Prates;
Santa Amélia;
Nova Suíça;
Castelo Manacás;
Com todas listadas acima dando 100% de bolsa.

Para rematrícula: todas unidades dão bolsas que vão até 100%.

Então foi feita a média das bolsas de cada unidade usando o seguinte cálculo:


<pre lang="Python">médiaNovaMatrícula = novaMatrícula.groupby('Unidade').agg(
    Soma = ('Bolsa', 'sum'),
    numDescontos = ('Bolsa' , 'count')
)
médiaNovaMatrícula['média'] = round(médiaNovaMatrícula['Soma']/médiaNovaMatrícula['numDescontos'])

médiaRematrícula = rematrícula.groupby('Unidade').agg(
    Soma = ('Bolsa', 'sum'),
    numDescontos = ('Bolsa' , 'count')
)
médiaRematrícula['média'] = round(médiaRematrícula['Soma']/médiaRematrícula['numDescontos'])</pre>


### Resultados


<img width="780" height="540" alt="image" src="https://github.com/user-attachments/assets/eb890ed6-4947-4ced-b3a0-cf99077ad1c9" />


<img width="780" height="540" alt="image" src="https://github.com/user-attachments/assets/b2f977c1-df70-41db-9b73-c8d4aae56b63" />


<img width="1389" height="859" alt="image" src="https://github.com/user-attachments/assets/64f5890c-12b6-46bc-be69-883ffc90c929" />



O resultado obtido foi: 

As novas matrículas tiveram uma vantagem ligeira em média de descontos. 
É legal observar que a unidade Carajás foi a que mais deu descontos e a que mais teve matrículas.

A quantidade desconstos não parece ter muita relação com o número de matrículas nos casos além dp Carajás.


##  Conclusão

Foi possível perceber com a análise que existe uma diferença entre as novas matrículas e as rematrículas.
Diferença que é necessária ser considerada para as estratégias de negócios.

