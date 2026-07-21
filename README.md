# CleanTex-Poster

Um template LaTeX modular, moderno e *plug-and-play* para criação de pôsteres em tamanho A0 com macros pré-configuradas para *fancy* colorboxes. A ideia é manter a filosofia *idiot-proof*, automatizando a compilação para evitar problemas clássicos do LaTeX em formatos gigantes.

## 🚀 Quickstart

A compilação requer tanto o pdfLaTeX quanto o [Biber](https://github.com/plk/biber).

Caso queira usar localmente (recomendado), baixe o [arquivo zip](https://github.com/timotheosf/CleanTeX-Poster/archive/refs/heads/main.zip) ou clone o repositório:
```bash
git clone https://github.com/seu-usuario/CleanTex-Poster.git
```

A melhor opção de compilação é usar o [Latexmk](https://mgeier.github.io/latexmk.html):
```bash
latexmk -pdf main.tex 
```
Ou a receita tradicional:
```bash
pdflatex main.tex
biber main
pdflatex main.tex
pdflatex main.tex
```

**Manual de uso rápido**:
1. **Metadados:** preencha o arquivo `_setup.tex` com o título, autores e contatos. Os logos do cabeçalho se ajustam sozinhos.
2. **Conteúdo:** escreva o seu pôster dentro do arquivo `content.tex`.
3. **Bibliografia:** adicione suas referências no arquivo `_bibliography/references.bib`. O template já está configurado para imprimir todas as referências (`\nocite{*}`) adicionadas.
4. **Logos:** adicione a logo do seu grupo/laboratório na pasta `_logos/`. Para usá-la no cabeçalho, basta abrir o main.tex e passar o nome do arquivo como argumento no comando de título (ex: `\BuildTitle[minha_logo]`).

## 🌲 Árvore de Diretórios

A lógica tipográfica, o ajuste fino de tamanhos e a arquitetura de caixas ficam blindados na pasta `_preamble`.

```Text
CleanTex-Poster/
├── _preamble/
│   ├── config.tex              # Lógica de construção do cabeçalho e referências.
│   ├── packages.tex            # Pacotes (math, tikz, fontes, margens, etc).
│   ├── standard_notation.tex   # Macros para padronizar notações matemáticas.
│   └── appearance_config.tex   # Motor de cálculo de fontes e design das ColorBoxes.
├── _logos/
│   └── ...                     # <-- Adicione aqui as logos que precisar
├── _bibliography/
│   └── references.bib          # Arquivo .bib com suas referências.
│
├── _setup.tex                  # Configuração de título, autores e contatos.
├── main.tex                    # Ponto de entrada do documento. Totalmente limpo.
└── content.tex                 # Arquivo principal.
```

## :shipit: Manual de Uso

### 1. ⚙️ Dados do Cabeçalho (`_setup.tex`)
Edite as variáveis abaixo para gerar automaticamente o cabeçalho superior do pôster. O template calcula as margens e a centralização sozinho.

```latex
\PosterTitle{Título do pôster}
\PosterAuthors{
    Autor Um\textsuperscript{1}$^\dagger$,
    Autor Dois\textsuperscript{1}, e 
    Autor Três\textsuperscript{1}
}
\PosterContacts{
    \textsuperscript{1}Departamento de Física, Universidade Federal de Viçosa --- UFV\\[0.2cm]
    $^\dagger$\mbox{\href{mailto:email@ufv.br}{{\faEnvelope[regular]}\hspace{0.13cm} email@ufv.br}}
}
```

### 2. 🖼️ Personalizando as Logos do Cabeçalho (`main.tex`)
A inserção da logo do seu laboratório (no lado direito do cabeçalho) é totalmente automatizada. 
1. Coloque a imagem na pasta `_logos/` (ex: `minha_logo.png`).
2. No arquivo principal `main.tex`, chame a macro `\BuildTitle` passando o nome do arquivo (sem a extensão) como argumento opcional:

```latex
\BuildTitle[minha_logo]
```
**Nota:** O template possui comportamentos especiais programados no `_preamble/config.tex`. Por exemplo, ao compilar com `\BuildTitle[lespa]`, o template não apenas carrega a logo do LESPA, mas também ajusta a largura da coluna e imprime o nome do laboratório por extenso automaticamente.

### 3. 📦 Caixas de Destaque (ColorBoxes)
O texto do pôster flui em 3 colunas (gerenciadas pelo pacote `multicol`). Para organizar visualmente seus métodos e resultados, o template fornece 4 caixas prontas para uso no arquivo `content.tex`:

```latex
% Caixa Azul com título sobreposto
\begin{bluebox}{Título da Caixa}
    Seu texto aqui...
\end{bluebox}

% Caixa Branca (estilo Floral/Cinza)
\begin{floralbox}{Título da Caixa} ... \end{floralbox}

% Caixa Cinza (Background Gainsboro)
\begin{graybox}{Título da Caixa} ... \end{graybox}

% Caixa Escura (Ideal para Referências e Agradecimentos)
\begin{darkbox}{Título da Caixa} ... \end{darkbox}
```
Se quiser centralizar o título da caixa, basta passar o argumento `[center title]`, exemplo: `\begin{darkbox}[center title]{Referências}`.



---
## Licença
[MIT License](LICENSE) - Sinta-se livre para usar, modificar e distribuir. Não é necessário citar a fonte.