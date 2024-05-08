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

Uma das informações que podemos ver e analisar é sobre os valores que são cobrados, e podemos analisar que metade dos cursos oferecidos são com o valor innferior a 35,00 Dolares. 
![download](https://github.com/ViniSegatto/Projeto-Aplicado-3/assets/117327390/ec46ba65-d4dd-4225-8463-7e35360f8af2)

Podemos ver que temos muitos dados, com mais de 200k de linhas, com pouquissimos valores nulos, o que não serão um problema, pois iremos tratar os dados antes de criarmos o nosos modelo de recomendação.

