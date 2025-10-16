# Visualizador 2D com Algoritmos de Recorte (Clipping)

Um projeto de computação gráfica que implementa **algoritmos de recorte (clipping)** para visualização de objetos geométricos 2D. O sistema oferece uma pipeline completa de transformação geométrica com múltiplos algoritmos de clipping e uma interface interativa para navegação e análise.

## 📸 Screenshots da Aplicação

### Tela Inicial
![Tela Inicial](screenshots/tela_inicial.png)
*Interface principal com controles de navegação, zoom, rotação e seleção de algoritmos*

### Tela com Recorte
![Tela com Recorte](screenshots/tela_recorte.png)
*Visualização dos objetos após aplicação dos algoritmos de clipping*

### Display List
![Display List](screenshots/display_list.png)
*Tabela detalhada mostrando coordenadas em todos os sistemas (Mundo, PPC, Viewport)*

### Controles do Teclado
![Controles do Teclado](screenshots/controles_teclado.png)
*Informações sobre o projeto e instruções de uso*

## 📋 Descrição

Este projeto implementa uma **pipeline completa de transformação geométrica** com foco em **algoritmos de recorte (clipping)**. O sistema demonstra conceitos avançados de computação gráfica através de:

### 🔧 Funcionalidades Principais
- **Pipeline de Transformação**: Mundo → PPC → Clipping → Viewport → Desenho
- **Algoritmos de Clipping para Linhas**: Cohen-Sutherland e Liang-Barsky (selecionáveis)
- **Algoritmo de Clipping para Polígonos**: Weiler-Atherton
- **Sistema de Coordenadas PPC**: Projeção Paralela Canônica com centro na origem
- **Transformações Interativas**: Navegação, zoom e rotação em tempo real
- **Display List Detalhado**: Visualização de coordenadas em todos os sistemas
- **Interface Gráfica Avançada**: Controles intuitivos e feedback visual

## 🛠️ Tecnologias Utilizadas

- **Python 3.x** - Linguagem principal
- **Tkinter** - Interface gráfica nativa
- **xml.etree.ElementTree** - Parsing de arquivos XML
- **math** - Operações matemáticas para transformações
- **Jupyter Notebook** - Ambiente de desenvolvimento interativo

## 📁 Estrutura do Projeto

```
CG2/
├── ideia_interface.ipynb              # Código principal (Jupyter Notebook)
├── entrada.xml                        # Arquivo de exemplo básico
├── teste.xml                          # Arquivo de teste com casos extremos
├── screenshots/                       # Pasta com capturas de tela da aplicação
│   ├── tela_inicial.png              # Screenshot da tela inicial
│   ├── tela_recorte.png              # Screenshot da tela com recorte
│   ├── display_list.png              # Screenshot do display list
│   └── sobre.png                     # Screenshot da tela sobre
├── RELATÓRIO _ TRABALHO PRÁTICO 2.pdf # Relatório técnico completo
└── README.md                          # Este arquivo
```

## 🚀 Como Executar

### Pré-requisitos
- **Python 3.x** instalado
- **Jupyter Notebook** ou **JupyterLab**
- Bibliotecas padrão do Python (tkinter, xml, math)

### Executando o projeto

1. **Via Jupyter Notebook** (recomendado):
   ```bash
   jupyter notebook ideia_interface.ipynb
   ```
   Execute a célula de código para iniciar a aplicação.

2. **Via JupyterLab**:
   ```bash
   jupyter lab ideia_interface.ipynb
   ```

3. **Via Python direto**:
   Extraia o código da célula Python do notebook e salve em um arquivo `.py`, então execute:
   ```bash
   python visualizador_clipping.py
   ```

## 📋 Formato do Arquivo XML

O sistema aceita arquivos XML com a seguinte estrutura:

```xml
<?xml version="1.0" ?>
<dados>
    <!-- Configuração da viewport -->
    <viewport>
        <vpmin x="0" y="0"/>
        <vpmax x="800" y="600"/>
    </viewport>
    
    <!-- Configuração da window (mundo) -->
    <window>
        <wmin x="-100.0" y="-75.0"/>
        <wmax x="100.0" y="75.0"/>
    </window>

    <!-- Objetos geométricos com cores opcionais -->
    <ponto cor="Light Coral" x="0" y="0"/>
    
    <reta cor="Teal">
        <ponto x="-300" y="-200"/>
        <ponto x="300" y="200"/>
    </reta>
    
    <poligono cor="Green">
        <ponto x="-140" y="-60"/>
        <ponto x="0" y="120"/>
        <ponto x="140" y="-60"/>
    </poligono>
</dados>
```

### Elementos Suportados

- **`<viewport>`**: Define o tamanho da área de visualização em pixels
  - `vpmin`: Coordenada mínima (canto inferior esquerdo)
  - `vpmax`: Coordenada máxima (canto superior direito)

- **`<window>`**: Define a área do mundo que será visualizada inicialmente
  - `wmin`: Coordenada mínima do mundo
  - `wmax`: Coordenada máxima do mundo

- **`<ponto>`**: Define um ponto com coordenadas `x` e `y`
  - Atributo opcional `cor`: Define a cor do ponto

- **`<reta>`**: Define uma linha com dois pontos
  - Atributo opcional `cor`: Define a cor da linha
  - Sujeita aos algoritmos de clipping Cohen-Sutherland ou Liang-Barsky

- **`<poligono>`**: Define um polígono com três ou mais pontos
  - Atributo opcional `cor`: Define a cor do polígono
  - Sujeito ao algoritmo de clipping Weiler-Atherton

## 🎮 Controles

### Navegação
- **↑ ↓ ← →**: Mover a window (navegar pela cena)
- **+ / =**: Zoom in (aproximar)
- **- / _**: Zoom out (afastar)
- **< / ,**: Rotacionar para a esquerda
- **> / .**: Rotacionar para a direita

### Interface
- **Menu Arquivo > Abrir**: Carregar um arquivo XML
- **Botões de navegação**: Controles visuais para movimento
- **Botões de zoom**: Controles visuais para zoom
- **Botões de rotação**: Controles visuais para rotação
- **Radio buttons**: Seleção do algoritmo de clipping (Cohen-Sutherland / Liang-Barsky)
- **Botão Display List**: Abrir tabela detalhada de coordenadas
- **Botão Sobre**: Informações e instruções

## 🧮 Conceitos Implementados

### Pipeline de Transformação Geométrica

O sistema implementa uma pipeline completa de transformação:

**Mundo → PPC → Clipping → Viewport → Desenho**

#### 1. Transformação Mundo → PPC (Projeção Paralela Canônica)
- Translação para centralizar a window na origem
- Rotação baseada no ângulo atual
- Normalização para o sistema PPC [-w/2, w/2] × [-h/2, h/2]

#### 2. Algoritmos de Clipping no PPC

**Para Linhas:**
- **Cohen-Sutherland**: Algoritmo baseado em códigos de região
- **Liang-Barsky**: Algoritmo paramétrico mais eficiente

**Para Polígonos:**
- **Weiler-Atherton**: Algoritmo avançado para clipping de polígonos

#### 3. Transformação PPC → Viewport
- Mapeamento das coordenadas PPC normalizadas para pixels da tela
- Inversão do eixo Y para coordenadas de tela

### Componentes da Interface

1. **Viewport Principal**: Área de renderização dos objetos após clipping
2. **Painel de Controles**: Navegação, zoom, rotação e seleção de algoritmos
3. **Display List**: Tabela detalhada com coordenadas em todos os sistemas
4. **Informações em Tempo Real**: Algoritmo atual, posição da window, ângulo de rotação

## 📊 Funcionalidades

### ✅ Algoritmos de Clipping
- **Cohen-Sutherland** para linhas (baseado em códigos de região)
- **Liang-Barsky** para linhas (algoritmo paramétrico)
- **Weiler-Atherton** para polígonos (clipping avançado)
- Seleção dinâmica entre algoritmos de linha

### ✅ Pipeline de Transformação
- Transformação Mundo → PPC com rotação
- Clipping no sistema PPC
- Transformação PPC → Viewport
- Renderização final na tela

### ✅ Interface Interativa
- Navegação em tempo real (teclas e botões)
- Zoom in/out com limites inteligentes
- Rotação contínua da cena
- Carregamento de arquivos XML
- Display List detalhado com coordenadas

### ✅ Visualização Avançada
- Cores personalizáveis para objetos
- Feedback visual do algoritmo em uso
- Informações de posição e rotação em tempo real
- Suporte a objetos complexos e casos extremos

## 🔧 Estrutura do Código

### Classe Principal: `Visualizador`

#### Inicialização e Interface
- **`__init__`**: Configura interface gráfica e variáveis de estado
- **`abrir_arquivo`**: Diálogo para seleção de arquivo XML
- **`carregar_arquivo`**: Parser XML e configuração inicial

#### Pipeline de Transformação
- **`world_to_ppc`**: Transformação Mundo → PPC com rotação
- **`ppc_to_viewport`**: Transformação PPC → Viewport
- **`realizar_clipping`**: Aplica clipping a todos os objetos

#### Algoritmos de Clipping
- **`clip_reta_cohen_sutherland`**: Implementação Cohen-Sutherland
- **`clip_reta_liang_barsky`**: Implementação Liang-Barsky
- **`clip_poligono_weiler_atherton`**: Implementação Weiler-Atherton
- **`calcular_region_code`**: Códigos de região para Cohen-Sutherland

#### Controles Interativos
- **`_mover_e_recarregar`**: Navegação pela cena
- **`_zoom`**: Zoom in/out com limites
- **`_rotacionar`**: Rotação da cena
- **`_atualizar_algoritmo`**: Troca de algoritmo de clipping

#### Visualização
- **`desenhar_viewport`**: Renderização principal
- **`atualizar_displaylist`**: Atualização da tabela de coordenadas
- **`mostrar_sobre`**: Janela de informações

## 🎯 Exemplo de Uso

### Fluxo Básico
1. **Execute a aplicação** via Jupyter Notebook
2. **Carregue um arquivo XML** usando "Arquivo > Abrir"
3. **Selecione o algoritmo de clipping** (Cohen-Sutherland ou Liang-Barsky)
4. **Navegue pela cena** usando setas ou botões
5. **Experimente zoom e rotação** para ver o clipping em ação
6. **Abra o Display List** para ver coordenadas detalhadas
7. **Compare algoritmos** alternando entre Cohen-Sutherland e Liang-Barsky

### Arquivos de Exemplo Disponíveis

#### `entrada.xml` - Exemplo Básico
- Objetos simples para demonstração inicial
- Window pequena para visualização clara
- Ideal para entender os conceitos básicos

#### `teste.xml` - Casos Extremos
- **Stress test** com muitas linhas longas
- **Casos limítrofes**: linhas paralelas às bordas
- **Precisão numérica**: linhas quase colineares
- **Diagonais extremas**: atravessando cantos
- **Window ampla** (-100 a 100 em X, -75 a 75 em Y)
- Ideal para testar robustez dos algoritmos

### Dicas de Uso
- Use **zoom** para focar em áreas específicas e ver detalhes do clipping
- **Rotacione** a cena para ver como os algoritmos se comportam em diferentes orientações
- **Compare algoritmos** em tempo real para entender diferenças de performance
- **Analise o Display List** para entender as transformações de coordenadas

## 📚 Conceitos de Computação Gráfica

Este projeto demonstra conceitos avançados de computação gráfica:

### Algoritmos de Clipping
- **Cohen-Sutherland**: Eficiente para casos simples, baseado em códigos de região
- **Liang-Barsky**: Mais eficiente para casos complexos, baseado em equações paramétricas
- **Weiler-Atherton**: Algoritmo sofisticado para clipping de polígonos

### Pipeline de Transformação
- **Sistema de Coordenadas Múltiplos**: Mundo, PPC, Viewport
- **Projeção Paralela Canônica (PPC)**: Normalização para clipping eficiente
- **Transformações Geométricas**: Translação, rotação, escala
- **Homogeneização**: Uso de coordenadas homogêneas para transformações

### Técnicas Avançadas
- **Clipping no PPC**: Otimização através de normalização
- **Códigos de Região**: Classificação rápida de pontos
- **Algoritmos Paramétricos**: Cálculo eficiente de interseções
- **Robustez Numérica**: Tratamento de casos limítrofes

### Interface e Visualização
- **Rendering em Tempo Real**: Atualização dinâmica da visualização
- **Display List**: Estrutura de dados para análise detalhada
- **Feedback Visual**: Indicação do algoritmo e estado atual

## 🎓 Objetivos Educacionais

Este projeto foi desenvolvido para demonstrar:

- **Implementação prática** de algoritmos clássicos de clipping
- **Comparação de performance** entre diferentes algoritmos
- **Pipeline completa** de transformação geométrica
- **Tratamento de casos extremos** e robustez numérica
- **Interface interativa** para experimentação e aprendizado

## 📄 Licença

Este projeto é desenvolvido para fins educacionais em computação gráfica.

---

**Desenvolvido como parte do estudo de Computação Gráfica - Algoritmos de Recorte (Clipping)**

**Trabalho Prático 2 - Implementação de Algoritmos de Clipping**
