# Projeto-Aplicado-3
# Modelo Recomendação.
Neste projeto para terminar o 4° semestre do nosso curso de Ciência de Dados pela Universidade Presbiteriana Mackenzie, fomos desafiados a fazer um modelo de recomendação, e decidimos por fazer o projeto baseado no [dataset](https://www.kaggle.com/datasets/hossaingh/udemy-courses?select=Course_info.csv)
disponivel na plataforma [Kaggle](https://www.kaggle.com/) sobre cursos disponiveis na plataforma [Udemy](https://www.udemy.com). 

# Sobre o Dataset

# Conteudo e estrutura do Dataset

Este dataset consiste em informações sobre diversos cursos que são oferecidos ou vendidos pela plataforma Udemy, e conta com dados desde 2010 até 2022.

As colunas desse dataset são:													

id: Numero de identificação do curso.

title: em portugues "Título" do curso.

is_paid: Indica se o curso é pago ou gratuito.

price: indica o "Preço" (se o curso for pago).

headline: Título resumido do curso.

num_subscribers: Número de inscritos.

avg_rating: Classificação média.

num_reviews: Número de avaliações.

num_comments: Número de comentários.

num_lectures: Número de aulas.

content_length_min: Duração total do conteúdo (em minutos).

published_time: Data de publicação.

last_update_date: Data da última atualização.

category: Categoria do curso.

subcategory: Subcategoria do curso.

topic: Tópico do curso.

language: Idioma do curso.

course_url: URL do curso.

instructor_name: Nome do instrutor.

instructor_url: URL do instrutor.

# Principais Características do Conjunto de Dados:

Número de Cursos: 209.734
Número de Instrutores: 73.514
Número de Idiomas: 79
Número de Categorias: 13
Data de Coleta dos Dados: 10 de outubro de 2022


Na coluna "category" categorias temos dados importantes de quais são as areas nas quais temos cursos relacionados, e são essas areas: Development, IT & Software, Teaching & Academics, Business, Personal Development, Design, Health & Fitness, Marketing, Lifestyle, Finance & Accounting, Office Productivity, Music, Photography & Video. 

# Iniciando com uma breve (EDA) Exploratory Data Analysis

Para a criação desse modelo começamos com uma (EDA) Exploratory Data Analysis, para que possamos entender melhor os dados que estamos lidando 
![image](https://github.com/ViniSegatto/Projeto-Aplicado-3/assets/117327390/b70d1472-9e32-4c21-ad04-40e5e355950b)
![image](https://github.com/ViniSegatto/Projeto-Aplicado-3/assets/117327390/782683db-58a6-4e0f-b1e5-9a5ec71bbf53)
![image](https://github.com/ViniSegatto/Projeto-Aplicado-3/assets/117327390/965bf413-86fd-495c-8359-7a4b1912072b)

Podemos ver que temos muitos dados, com 209.734 linhas, com pouquissimos valores nulos, o que não serão um problema, pois iremos tratar os dados antes de criarmos o nosos modelo de recomendação, além de que a maioria dos valores nulos são da coluna de "Data da ultima atualização" o que nos mostra apenas que o curso não foi atualizado.

Uma das informações que podemos ver e analisar é sobre os valores que são cobrados, e podemos analisar que metade dos cursos oferecidos são com o valor innferior a 35,00 Dolares. 
![download](https://github.com/ViniSegatto/Projeto-Aplicado-3/assets/117327390/ec46ba65-d4dd-4225-8463-7e35360f8af2)


# Começando o tratamento para criação do nosso modelo. 

Por motivos de hardware, este dataset contem muitos dados, nos quais exigia um uso de memoria muitissimo alto, mais de 120GBs de RAM, então por esse motivo, tive que escolher dados relevantes para criar um modelo de recomendação, venha comigo que no caminho eu explico. 

Como podemos ver no nosso arquivo de notebook, na parte 2, comecei por vendo quais as quantidas em soma e porcentagens de dados unicos que continham na coluna "language" e "category", e como podemos analisar, mais de 50% dos dados são em lingua Inglesa,, seguido por Portugues e Espanhol com pouco mais de 8% em ambos, e para completar o top 5 temos Turco e Japones com 3% cada. Assim para não termos uma dispersão muito grande dos dados, e para enxutar nossos dados para o modelo, resolvi descartar as outras 67 linguas, mas mantendo 75% dos nossos dados. 
Em seguida ao analisar as categorias que possuimos nesse dataset, optei por deixar tambem o Top 5 das categorias que mais aparecem em nosso dataset, mantendo assim ainda 50% de todos os dados com as ccategorias: 'Desenvolvimento', 'TI e Software', 'Ensino e Acadêmico', 'Negócios', 'Desenvolvimento Pessoal'.

Na seção 2.1 dos nosso notebook, arrumei as datas para que ficasse mais claro para vermos as datas de lançamentos e de atualizações dos cursos. 
E infelizmente como nosso dataset continua ainda muito grande, resolvi por deixar apenas os cursos lançados apenas a partir de 2019, por se tratar de cursos de tecnologia e derivados, como o mercado muda e se atualiza muito rapido, optei por deixar apenas os dados mais recentes.

Na seção 2.2, analisei a quantidade de dados nas colunas "avg_rating" e "num_reviews", para assim poder selecionar cursos com certas avaliações positivas, acima de 3,75, e com pelo menos mais de 10 avaliações, para que possa ter uma quantidade razoavel de avaliações. 

Agora após realizarmos essa filtragem dos dados, podemos começar a criar nosso modelo, optei por criar um modelo no qual recomende cursos com base em seus Titulos, para que assim possa realizar uma recomendação mais acertiva com as palavras chaves.

![image](https://github.com/ViniSegatto/Projeto-Aplicado-3/assets/117327390/6d77d0aa-1261-45d9-9829-5c40a898ba16)

Começamos importando a biblioteca neattext, que fornece funções úteis para trabalhar com texto de forma limpa e organizada. 

import neattext.functions as nfx: Usamos isso para importar a biblioteca neattext e renomeia o módulo functions como nfx. Isso permite acessar as funções fornecidas pela biblioteca usando o prefixo nfx.
dir(nfx): Aqui chamamos a função dir() para listar todos os atributos e métodos disponíveis no módulo nfx. Isso incluirá todas as funções disponíveis na biblioteca neattext que podem ser usadas para manipulação e limpeza de texto.


Portanto, esse código essencialmente lista todas as funções disponíveis na biblioteca neattext, o que será útil para eenxugar textos, emojis e simbolos para facilitar ainda mais e deixar apenas as palavras que realmente importam para a recomedação.
