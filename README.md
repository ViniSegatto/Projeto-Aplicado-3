# Modelo Recomendação
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

Abaixo aqui podemos ver como o tratamendo dos dados ajudar a enxugar os dados do titulo.
![image](https://github.com/ViniSegatto/Projeto-Aplicado-3/assets/117327390/129ebdef-219c-450e-8f17-92072bfb4412)

Utilizamos as linhas abaixo nas quais explicarei suas utilidades para a criação desse modelo: 

count_vect = CountVectorizer(). Isso cria uma instância do objeto CountVectorizer da biblioteca scikit-learn. CountVectorizer é usado para converter uma coleção de documentos de texto em uma matriz de contagens de tokens.

cv_mat = count_vect.fit_transform(df['title_limpo']). Aqui, o método fit_transform do objeto CountVectorizer é usado para ajustar o vetorizador aos dados de texto na coluna 'title_limpo' do DataFrame df e transformá-lo em uma matriz de contagem de palavras. A matriz resultante é atribuída à variável cv_mat.

cv_mat. Isso imprime a matriz resultante após a transformação pelo CountVectorizer. Esta matriz contém contagens de ocorrências de tokens (palavras) nos documentos de texto.

cv_mat.todense(). O método todense() é chamado na matriz cv_mat para converter a matriz esparsa em uma matriz densa, o que facilita a visualização e a manipulação dos dados.

df_cv_words = pd.DataFrame(cv_mat.todense(),columns=count_vect.get_feature_names_out()): Isso cria um DataFrame do pandas chamado df_cv_words a partir da matriz densa resultante da contagem de palavras. Os nomes das colunas do DataFrame são definidos como os tokens (palavras) extraídos dos documentos de texto usando o método get_feature_names_out() do objeto CountVectorizer.

df_cv_words.head(). Isso exibe as primeiras linhas do DataFrame df_cv_words, mostrando as contagens de palavras para os documentos de texto processados. Cada linha representa um documento e cada coluna representa uma palavra, com o valor indicando quantas vezes a palavra ocorre no documento correspondente.

cosine_sim_mat = cosine_similarity(cv_mat). Isso calcula a matriz de similaridade do cosseno entre os vetores de documentos representados pela matriz de contagem de palavras cv_mat. A similaridade do cosseno é uma medida comum usada para determinar a semelhança entre dois vetores de alta dimensão.

scores = list(enumerate(cosine_sim_mat[idx])). Aqui, os escores de similaridade entre o curso fornecido (identificado pelo índice idx) e todos os outros cursos são extraídos da matriz de similaridade do cosseno. Os índices dos cursos e seus escores correspondentes são armazenados em uma lista.

sorted_scores = sorted(scores,key=lambda x:x[1],reverse=True). Os escores de similaridade são classificados em ordem decrescente com base nos valores de similaridade.

selected_course_indices = [i[0] for i in sorted_scores[1:]]. Aqui, os índices dos cursos recomendados são extraídos da lista classificada de escores de similaridade. O primeiro curso é excluído porque é o próprio curso fornecido.

selected_course_scores = [i[1] for i in sorted_scores[1:]]. Os escores de similaridade correspondentes aos cursos recomendados são armazenados em uma lista separada.

recommended_result = df['title'].iloc[selected_course_indices]. Os títulos dos cursos recomendados são extraídos do DataFrame original df com base nos índices dos cursos recomendados.

rec_df = pd.DataFrame(recommended_result). Um novo DataFrame chamado rec_df é criado com os títulos dos cursos recomendados.

rec_df['similarity_scores'] = selected_course_scores. Os escores de similaridade correspondentes são adicionados ao DataFrame rec_df para fornecer informações sobre a similaridade de cada curso recomendado com o curso fornecido.

![image](https://github.com/ViniSegatto/Projeto-Aplicado-3/assets/117327390/2ff74648-9e4c-4806-9056-9525bbd7b6be)

Com todos esses dados acima, podemos criar uma função para usarmos o modelo de recomendação para recomendar os cursos que são mais proximos de acordo com a sua escolha de curso. 

# Recomendações 

Observe como nosso modelo de recomendação funciona! Com o curso "Oracle Process Cloud (PCS)" como referência, ele identificou os cursos mais relevantes e suas pontuações de compatibilidade. As pontuações refletem a probabilidade de você gostar desses cursos, com base na sua escolha de curso. 

![image](https://github.com/ViniSegatto/Projeto-Aplicado-3/assets/117327390/3e9d36d5-ccde-457f-9109-1f17a7b8986a)

# Conclusão

Apesar dos desafios em treinar o modelo com um conjunto de dados extenso, superamos essa etapa e criamos um sistema de recomendação personalizado para cada usuário. Essa funcionalidade agrega valor à plataforma ao oferecer cursos relevantes com base em suas preferências e histórico de aprendizado. Essa estratégia aumenta o engajamento com os cursos e, consequentemente, as chances de conversão em vendas.



E se você chegou até aqui, você pode me encontrar tambem nas seguintes redes abaixo! 

[Linkedin](https://www.linkedin.com/in/vinicius-segatto-9a560421b/)

[Medium](https://medium.com/@viniciussegatto11)

[Github](https://github.com/ViniSegatto)

Obrigado.
