# Projeto QGIS — Análise Geoespacial de Gleba com Planejamento de Plantio e Zoneamento Urbano

Este repositório contém um projeto QGIS desenvolvido para fins de análise geoespacial de uma gleba (talão de terra) na região de Teresina — PI, integrando dados de planejamento agrícola, modelo digital de elevação (MDE) e informações de zoneamento urbano municipal.

---

## 📋 Visão Geral

O projeto reúne as seguintes funcionalidades:

- Delimitação e análise da gleba (perímetro e área em hectares)
- Geração e análise de linhas de plantio
- Grade amostral de campo (pontos de amostragem georreferenciados)
- Curvas de nível (cotas de elevação) extraídas do MDE
- Modelo Digital de Elevação (MDE) e mapa de sombreamento (hillshade)
- Zoneamento urbano de Teresina conforme a Lei nº 5.807/2022
- Perímetro Urbano de Teresina conforme a Lei nº 3.757 de 03/06/2022
- Zonas de Urbanização Específica

---

## 🛠️ Requisitos

| Software | Versão mínima recomendada |
|---|---|
| [QGIS](https://qgis.org/) | 3.28 LTR ou superior (projeto criado no QGIS 3.40.13-Bratislava) |

Não são necessários plugins adicionais para visualizar o projeto. Todas as camadas já estão incluídas no repositório.

---

## 🚀 Como Abrir o Projeto

1. Clone ou baixe este repositório em seu computador.
2. Abra o QGIS.
3. No menu **Projeto → Abrir**, navegue até a pasta do repositório e selecione o arquivo `qgis_projeto.qgz`.
4. O QGIS carregará automaticamente todas as camadas configuradas com seus estilos e sistemas de referência.

> **Atenção:** Mantenha todos os arquivos do repositório na mesma pasta. Se mover ou renomear arquivos, as camadas podem aparecer como não encontradas no QGIS.

---

## 📂 Estrutura do Repositório

```
QGIS-PROJETO/
│
├── qgis_projeto.qgz                  # Arquivo principal do projeto QGIS
│
├── talao_terra_UTM.*                  # Gleba (polígono) — SIRGAS 2000 / UTM Zona 24S
├── talão_terra_teresina.*             # Gleba (versão em WGS 84)
│
├── linha_plantio_final.*             # Linhas de plantio finais (252 linhas)
├── linha_plantio.*                   # Linha de plantio base
├── linha_plantio1.*                  # Parcial — etapa 1 (101 linhas)
├── linha_plantio2.*                  # Parcial — etapa 2 (151 linhas)
│
├── grade_amostral.*                  # Grade amostral (16 pontos)
├── grade_amostral_1.*                # Grade amostral revisada (15 pontos)
├── grade_amostral_1_wgs.*            # Grade amostral em WGS 84 com lat/long
├── grade_amostral_rec.*              # Recorte da grade amostral
├── grade_amostral_recorte.*          # Grade amostral recortada
│
├── COTA ELEVACAO.gpkg                # Curvas de nível (GeoPackage — camada: contour)
│
├── MODELO MDE TESTE.tif              # MDE — modelo digital de elevação (teste)
├── TESTE MDE.tif                     # MDE alternativo
├── sombreamento.tif                  # Mapa de sombreamento (hillshade) gerado a partir do MDE
├── raster_teste_teresina.tif         # Raster de referência da área de Teresina
│
├── ZONEAMENTO-Lei-5.807-2022/
│   └── Zoneamento-Lei-5.807-2022.*   # Zoneamento urbano (26 zonas) — SIRGAS 2000 / UTM Zona 23S
│
├── ZONA_URBANIZACAO_ESPECIFICA/
│   └── ZONA_URBANIZACAO_ESPECIFICA.* # Zonas de urbanização específica (3 zonas)
│
└── Perimetro Urbano 2022 Lei nº3.757 de 03-06-2022/
    └── Perimetro-Urbano2022.*        # Perímetro urbano de Teresina — SIRGAS 2000 / UTM Zona 23S
```

---

## 🗺️ Descrição das Camadas

### 🏞️ Gleba (Talão de Terra)
Polígono representando a área da propriedade rural analisada. Contém os atributos de **área (ha)** e **perímetro (km)**.

- Arquivo: `talao_terra_UTM.shp`
- Sistema de Referência: WGS 1984 / UTM Zona 24S (EPSG:32724)

---

### 🌾 Linhas de Plantio
Linhas geradas para orientar o plantio na gleba. A camada final (`linha_plantio_final.shp`) contém **252 linhas** com atributos de identificador, instância, deslocamento (offset), camada de origem e caminho.

- Arquivos: `linha_plantio_final.shp`, `linha_plantio1.shp`, `linha_plantio2.shp`
- Sistema de Referência: WGS 1984 / UTM Zona 24S (EPSG:32724)

---

### 📍 Grade Amostral
Conjunto de pontos de amostragem distribuídos sobre a gleba para coleta de dados de campo. Contém coordenadas geográficas (latitude/longitude) e coordenadas planas UTM.

- Arquivos: `grade_amostral_1_wgs.shp` (15 pontos em WGS 84)
- Sistema de Referência: WGS 84 geográfico (EPSG:4326)

---

### 📈 Curvas de Nível (Cotas de Elevação)
Linhas de contorno de elevação extraídas do MDE, armazenadas em formato GeoPackage. Cada feição possui o atributo **COTA** (valor de elevação em metros).

- Arquivo: `COTA ELEVACAO.gpkg` (camada: `contour`)
- Sistema de Referência: WGS 84 (EPSG:4326)

---

### 🏔️ Modelo Digital de Elevação (MDE) e Sombreamento
Rasters de elevação do terreno com valores entre aproximadamente **51 m e 146,5 m**. O arquivo de sombreamento (`sombreamento.tif`) é derivado do MDE e utilizado para visualização tridimensional do relevo.

- Arquivos: `MODELO MDE TESTE.tif`, `TESTE MDE.tif`, `sombreamento.tif`, `raster_teste_teresina.tif`

---

### 🏙️ Zoneamento Urbano — Lei nº 5.807/2022
Polígonos representando as **26 zonas** do zoneamento urbano do município de Teresina, conforme a Lei nº 5.807/2022. Cada zona possui os atributos: macrozona, nome da zona, sigla, índice de aproveitamento (IA) e taxa de permeabilidade mínima (PM).

Exemplos de zonas presentes:
- Zona de Ocupação Moderada (ZOM1, ZOM2, ZOM3, ZOM4)
- Zona de Serviço (ZS1, ZS2, ZS3)
- Zona de Interesse Ambiental (ZIA)
- Zona Especial de Uso Sustentável (ZEUS)
- Zona de Desenvolvimento de Corredor Sudeste (ZDCSE)
- Zona Especial do Polo Cerâmico (ZEICP)

- Arquivo: `ZONEAMENTO-Lei-5.807-2022/Zoneamento-Lei-5.807-2022.shp`
- Sistema de Referência: SIRGAS 2000 / UTM Zona 23S

---

### 🏘️ Zona de Urbanização Específica
Polígonos com as zonas de expansão urbana específica (Expansão Sul, Expansão Oeste e Expansão Norte).

- Arquivo: `ZONA_URBANIZACAO_ESPECIFICA/ZONA_URBANIZACAO_ESPECIFICA.shp`
- Sistema de Referência: SIRGAS 2000 / UTM Zona 23S

---

### 🗺️ Perímetro Urbano — Lei nº 3.757/2022
Polígono delimitando o perímetro urbano oficial de Teresina conforme a Lei nº 3.757 de 03/06/2022.

- Arquivo: `Perimetro Urbano 2022 Lei nº3.757 de 03-06-2022/Perimetro-Urbano2022.shp`
- Sistema de Referência: SIRGAS 2000 / UTM Zona 23S

---

## 🌐 Sistemas de Referência de Coordenadas (SRC)

| Dados | SRC | EPSG |
|---|---|---|
| Gleba e linhas de plantio | WGS 1984 / UTM Zona 24S | 32724 |
| Grade amostral (WGS) | WGS 84 Geográfico | 4326 |
| Zoneamento, perímetro urbano e ZUE | SIRGAS 2000 / UTM Zona 23S | 31983 |
| Curvas de nível (GPKG) | WGS 84 | 4326 |

> O QGIS realiza reprojeção dinâmica (on-the-fly) entre os sistemas de referência, portanto todas as camadas serão exibidas sobrepostas corretamente na tela do mapa.

---

## 📌 Observações

- Os arquivos `.aux.xml` são gerados automaticamente pelo QGIS/GDAL para armazenar estatísticas dos rasters e **não devem ser editados manualmente**.
- Os arquivos `.cpg` definem a codificação de caracteres dos shapefiles (UTF-8).
- O arquivo `qgis_projeto.qgz.qto3settings` armazena configurações locais do projeto e pode ser ignorado.

---

## 📄 Legislação de Referência

| Documento | Descrição |
|---|---|
| Lei nº 3.757, de 03/06/2022 | Define o Perímetro Urbano de Teresina |
| Lei nº 5.807/2022 | Institui o Zoneamento Urbano de Teresina |
