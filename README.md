# Projeto Semestral - Geolocalização e Mapas Digitais

## 👥 Integrantes do Grupo
* **Igor Improta Martinez da Silva** | RA: 21.00834-5
* **Lucas Gozze Crapino** | RA: 22.00667-2
* **Murillo Penha Strina** | RA: 22.00730-0

---

## 📍 Sobre o Projeto
Este projeto tem como objetivo realizar uma análise exploratória espacial e de inteligência de mercado com dados de estabelecimentos cadastrados no **Uber Eats** nos Estados Unidos. O limite municipal escolhido como foco geográfico foi a cidade de **Birmingham, Alabama**. 

O desenvolvimento foi estruturado em duas etapas principais:
* **Etapa 1 (T1):** Extração, limpeza, geocodificação e visualização da distribuição espacial inicial dos restaurantes.
* **Etapa 2 (T2):** Análise avançada de inteligência de mercado cruzando dados de acessibilidade (Zonas Residenciais), precificação de frete e métricas de Custo-Benefício.

## 💾 Fonte de Dados e Armazenamento
* **Origem:** Dataset público do Kaggle com registros do Uber Eats. Disponível neste [link](https://www.kaggle.com/datasets/thedevastator/the-ubereats-restaurant-dataset-over-100000-us-r).
* **Armazenamento:** * A base de dados bruta original encontra-se no arquivo `Ubereat_US_Merchant.csv`.
  * A base de dados final, tratada com filtros espaciais, imputação estatística e marcadores de inteligência de mercado gerados no T2, foi exportada e está armazenada no formato **GeoJSON** (`dados_birmingham_tratados.json`).

## 🛠️ Ferramentas Utilizadas
O projeto foi desenvolvido em **Python** no ambiente **Google Colab**. As bibliotecas empregadas foram:
* `pandas` e `numpy`: Tratamento, manipulação tabular e imputação estatística de dados ausentes.
* `geopandas` e `shapely`: Criação de geometrias (Pontos e Polígonos) e execução de filtros e cruzamentos espaciais (*Spatial Join* / *Point-in-Polygon*).
* `osmnx`: Extração do polígono do limite municipal e da malha de bairros residenciais oficiais via OpenStreetMap.
* `folium`: Geração de mapa interativo de marcadores.
* `matplotlib`: Geração de mapas cartográficos estáticos para análise de densidade e correlação.
* `pydeck`: Renderização de malhas hexagonais 3D interativas (`HexagonLayer`) para análise de densidade e elevação.

---

## 🚀 Como Executar o Projeto

Recomendamos fortemente a execução na plataforma **Google Colab** para garantir a compatibilidade e a renderização correta dos mapas interativos em 3D.

### Passo 1: Preparando o Ambiente
1. Acesse o [Google Colab](https://colab.research.google.com/) e faça o upload dos notebooks (`T1_geolocalizacao.ipynb` e `T2_geolocalizacao.ipynb`).
2. Faça o upload do arquivo base `Ubereat_US_Merchant.csv` diretamente para a raiz (pasta `/content/`) do Colab.

### Passo 2: Execução das Células
1. A primeira célula de cada notebook instalará as dependências necessárias (`osmnx`, `pydeck`).
2. Execute o restante dos Notebooks sequencialmente clicando em **"Ambiente de Execução" > "Executar tudo"**.
3. *Atenção:* O processamento do `Spatial Join` e o download da malha do OpenStreetMap podem levar alguns segundos.

### Passo 3: Visualização dos Resultados
* **Mapas Estáticos (Matplotlib):** Serão gerados diretamente no output das células.
* **Mapas 3D Interativos (Pydeck):** O arquivo HTML será gerado e renderizado diretamente no console do Colab, permitindo rotacionar o mapa com o botão direito do mouse.
* **Exportação (T2):** O notebook T2 fará o download automático do arquivo `dados_birmingham_tratados.json` ao final da execução.

---

## 🔮 Proposta para Análise Futura (Elaborada no T1)

A partir da exploração inicial e do tratamento de dados geográficos, isolamos com sucesso os estabelecimentos do Uber Eats operantes nos limites da cidade de Birmingham (Alabama). A visualização espacial revelou concentrações claras de restaurantes, bem como variações notáveis tanto nas avaliações dos clientes quanto nas taxas de entrega.

**Diretrizes para a Análise (Etapa T2):**
Embora os dados pertençam ao mercado norte-americano, o objetivo da próxima etapa será desenvolver e validar um **modelo de inteligência espacial que possa ser replicado no mercado brasileiro de delivery** (como iFood, Rappi, Keeta, entre outros). O foco será investigar a relação espacial entre Preço, Taxa de Entrega e Satisfação do Cliente.

As principais frentes de estudo com o auxílio de cruzamentos espaciais serão:
1. **Mapeamento do Custo-Benefício Espacial:** Investigar se existe uma correlação geográfica entre a categoria de preço do restaurante, o valor da entrega e a avaliação positiva. A hipótese é analisar se restaurantes em áreas mais nobres entregam uma melhor relação custo-benefício ou se as "joias escondidas" (baratos e bem avaliados) estão nas periferias.
2. **Impacto da Localização na Satisfação:** Avaliar se restaurantes mais distantes dos bairros e regiões mais populosas tendem a ter avaliações piores devido ao tempo de trânsito e resfriamento da comida.
3. **Viabilidade de Implementação no Brasil:** Utilizar os *insights* obtidos com este dataset para propor como serviços de delivery brasileiros poderiam usar análises de proximidade geométrica para otimizar suas próprias taxas de entrega.

---

## 🎯 Conclusão da Análise de Dados (Resultados T2)

A aplicação das técnicas de Geoprocessamento (`Spatial Join`, visualizações multivariadas e malhas hexagonais) permitiu comprovar que a distribuição de restaurantes e a precificação logística possuem forte dependência espacial. A partir dos dados extraídos e tratados para a cidade de Birmingham, destacamos as seguintes conclusões para a nossa inteligência de mercado:

1. **Acessibilidade vs. Zonas Residenciais:** O cruzamento espacial com a malha do *OpenStreetMap* evidenciou um distanciamento claro entre os locais de consumo e os de moradia. Apenas **11,2%** dos estabelecimentos operam fisicamente dentro de zonas residenciais. Isso indica que a vasta maioria dos restaurantes se concentra em corredores comerciais, forçando a dependência de serviços logísticos (delivery) para atender à população nos subúrbios.
2. **Distribuição do Custo-Benefício ("Joias Escondidas"):** Nossa métrica de avaliação identificou que **76,5%** dos restaurantes mantêm um alto padrão de custo-benefício (notas acima de 4.0 e taxas de entrega adequadas). Contudo, a projeção cartográfica (Matplotlib) revela que estes não estão distribuídos de forma homogênea. Eles se aglomeram nos centros, criando verdadeiros "desertos de delivery" de qualidade nas bordas da cidade.
3. **Mapeamento de Densidade (HexagonLayer):** A projeção em hexágonos 3D (Pydeck) corrobora a tese de concentração espacial extrema. Áreas de pico no mapa hexagonal mostram superoferta em pontos isolados da malha viária, enquanto a maior parte da área municipal não possui "elevação" alguma.

**Viabilidade e Impacto Estratégico:**
A metodologia validada neste estudo comprova a necessidade de plataformas de delivery (como *Uber Eats*, *iFood* e *Rappi*) utilizarem análises de proximidade geométrica contínuas. A grande lacuna habitacional identificada (onde a demanda reside, mas a oferta não está presente fisicamente) configura a oportunidade perfeita para a implantação de redes de *Dark Kitchens* descentralizadas, otimizando o frete, o tempo de entrega e a temperatura do alimento para o consumidor final.