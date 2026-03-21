## T1 - Geolocalização e Mapas Digitais

## 👥 Integrantes do Grupo
* **Igor Improta Martinez da Silva** | RA: 21.00834-5
* **Lucas Gozze Crapino** | RA: 22.00667-2
* **Murillo Penha Strina** | RA: 22.00730-0

---

## 📍 Sobre o Projeto
Este projeto tem como objetivo realizar uma análise exploratória espacial de dados de estabelecimentos cadastrados no **Uber Eats** nos Estados Unidos. O foco desta primeira etapa (T1) foi extrair, limpar e visualizar a distribuição geográfica de restaurantes, utilizando como recorte espacial o limite municipal da cidade de **Birmingham, Alabama**. 

Através das visualizações interativas e estáticas geradas, buscamos compreender a densidade dos restaurantes e analisar a relação espacial entre a localização, as avaliações dos clientes e as taxas de entrega cobradas.

## 💾 Fonte de Dados e Armazenamento
* **Origem:** Os dados foram obtidos através de um dataset público no Kaggle contendo registros de restaurantes do Uber Eats.
* **Armazenamento (T1):** Para esta etapa inicial, os dados estão armazenados localmente e disponibilizados junto à entrega no arquivo `Ubereat_US_Merchant.csv`. 
* *(Nota: Para a etapa T2, os dados tratados neste notebook serão migrados para um banco de dados PostgreSQL com a extensão espacial PostGIS).*

## 🛠️ Ferramentas Utilizadas
O projeto foi desenvolvido em **Python** utilizando o ambiente **Google Colab**. As principais bibliotecas empregadas foram:
* `pandas`: Tratamento e manipulação tabular dos dados lidos do CSV.
* `geopandas` e `shapely`: Criação de geometrias (Pontos e Polígonos) e execução de filtros espaciais (*Point-in-Polygon*).
* `osmnx`: Extração do polígono oficial do limite municipal de Birmingham via OpenStreetMap.
* `folium`: Geração do mapa interativo com marcadores e *popups* de informações de negócio (Preço, Avaliação, Taxa).
* `matplotlib`: Geração do mapa estático bivariado para análise de correlação espacial.

---

## 🚀 Como Executar o Projeto

Como o script foi projetado e testado no **Google Colab**, recomendamos fortemente a sua execução nesta plataforma para evitar problemas de compatibilidade ou falta de bibliotecas no ambiente local. Siga os passos abaixo:

### Passo 1: Preparando o Ambiente (Google Colab)
1. Acesse o [Google Colab](https://colab.research.google.com/) e faça o upload do arquivo `T1_geolocalizacao.ipynb` fornecido nesta entrega.
2. Abra o painel lateral esquerdo clicando no ícone de **Pasta (Arquivos)**.
3. Faça o upload do arquivo base de dados `Ubereat_US_Merchant.csv` diretamente para a raiz (pasta `/content/`) do Colab.

### Passo 2: Execução das Células
1. A primeira célula de código (`!pip install osmnx`) instalará as dependências necessárias que não vêm por padrão no Colab. Execute-a e aguarde a conclusão.
2. Após a instalação, você pode rodar o restante do Notebook sequencialmente clicando em **"Ambiente de Execução" > "Executar tudo"** (ou `Ctrl + F9`).
3. *Atenção:* O processamento do polígono da cidade e a leitura do CSV podem levar alguns segundos.

### Passo 3: Visualização dos Resultados
* **Mapa Interativo (Folium):** Ao rodar a célula correspondente, um mapa interativo aparecerá. Você pode dar zoom, navegar pela cidade de Birmingham e clicar nos agrupamentos de marcadores para ver os detalhes individuais de cada restaurante.
* **Mapa Estático (Matplotlib):** Será gerado no final do script, evidenciando através de cor e tamanho a relação entre as avaliações e as taxas de entrega na cidade.

---

## 🔮 Proposta para Análise Futura (T2)
A partir da exploração inicial e do tratamento de dados geográficos, isolamos com sucesso os estabelecimentos do Uber Eats operantes nos limites da cidade de Birmingham (Alabama). Através da visualização estática gerada acima, é possível notar padrões de distribuição espacial, confirmando a viabilidade do projeto. Observa-se uma forte concentração no corredor central e nordeste de Birmingham, com variação visual clara tanto nas avaliações quanto nas taxas de entrega.

Para a segunda fase do projeto, o foco será aprofundar a investigação geográfica voltada para a **acessibilidade urbana** e **inteligência de mercado**. As principais frentes de estudo serão:

* **Identificação de "Desertos de Delivery":** Cruzar a localização atual dos restaurantes mapeados com as zonas residenciais da cidade para descobrir se existem bairros habitados que sofrem com escassez de opções de entrega.
* **Análise de Precificação Espacial (Desigualdade de Acesso):** Investigar se existe um padrão geográfico claro que dite a variação das taxas de entrega. O objetivo é responder se moradores de regiões mais afastadas dos grandes centros comerciais pagam taxas sistematicamente mais altas, dificultando o acesso ao serviço.
* **Mapeamento de Oportunidades de Expansão:** Utilizar a relação entre a avaliação dos clientes e a densidade de restaurantes para apontar regiões com "demanda reprimida" — ou seja, locais ideais para a abertura de novos negócios focados em delivery (*Dark Kitchens*), onde a concorrência atual possui baixa qualidade ou cobra taxas abusivas.
