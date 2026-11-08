# 🔍 Unicode & Mojibake Inspector

> **Inspecione, diagnostique e higienize caracteres invisíveis, acentos corrompidos (*mojibake*) e normalizações Unicode (`NFC` / `NFD` / `NFKC` / `NFKD`) em tempo real — 100% *client-side* e sem dependências.**

O **Unicode & Mojibake Inspector** (`appUnicodeInspector.html`) é uma ferramenta web leve e responsiva projetada para engenheiros de software, analistas de dados e desenvolvedores que precisam diagnosticar bugs silenciosos causados por caracteres ocultos, corrupção de codificação entre sistemas legados e divergências de normalização Unicode.

## ✨ Principais Recursos

### 🔬 Inspeção e Diagnóstico em Tempo Real

* **Visão Raio-X (Revelador de Ocultos):** Expõe visualmente caracteres invisíveis e perigosos que quebram consultas SQL, validações de formulário, parsers JSON e tokens de API — incluindo *Zero-Width Space* (`ZWSP U+200B`), *Non-Breaking Space* (`NBSP U+00A0`), *Byte Order Mark* (`BOM U+FEFF`), *Soft Hyphen* (`SHY U+00AD`), marcas direcionais (*Trojan Source* `RLO U+202E`) e caracteres de controle ASCII.

* **Mapa Interativo de Code Points:** Exibe cada caractere individualmente com seu código oficial Unicode (`U+XXXX`), nome técnico, contagem de *UTF-16 code units* e sequência exata de bytes em **UTF-8 Hexadecimal**.

* **Detector Inteligente de Mojibake:** Identifica strings em UTF-8 que foram lidas ou gravadas incorretamente como Latin-1/Windows-1252 (ex.: `"AtenÃ§Ã£o"` $\rightarrow$ `"Atenção"`), inclusive em textos híbridos que misturam acentos corrompidos com emojis.

* **Análise de Forma Normal Unicode:** Detecta instantaneamente se o texto está em **NFC** (padrão Windows/Web/Linux), **NFD** (padrão macOS) ou em estado misto.

### 🛠️ 8 Comandos de Correção e Sanitização em 1 Clique

* **Normalização Unicode (`NFC`, `NFD`, `NFKC`, `NFKD`):** Padroniza caracteres compostos e decompostos para evitar falhas de comparação `===` ou buscas em bancos de dados entre diferentes sistemas operacionais.

* **Purgar Invisíveis:** Remove caracteres fantasmas e controles não imprimíveis preservando apenas quebras de linha, tabulações e espaços ASCII legítimos.

* **Consertar Mojibake:** Executa reversão binária Windows-1252/Latin-1 $\rightarrow$ UTF-8 sem gerar falsos positivos.

* **Desfazer Duplo-Mojibake:** Executa múltiplas passadas iterativas para recuperar textos submetidos a duas ou mais corrupções sucessivas (ex.: `"AtenÃƒÂ§ÃƒÂ£o"` $\rightarrow$ `"Atenção"`).

* **NBSP → Espaço ASCII:** Converte toda a família de espaços Unicode especiais para o espaço padrão ASCII (`0x20`).

* **Remover Diacríticos:** Remove acentos e cedilhas via decomposição NFD (ideal para geração de *slugs* e chaves).

* **Aspas & Travessões ASCII:** Substitui aspas tipográficas curvas (`“ ” ‘ ’`), travessões (`— –`) e reticências (`…`) por equivalentes ASCII simples (`" ' - ...`).

* **Remover Linhas Duplicadas:** Higieniza listas e logs mantendo a ordem da primeira ocorrência e o padrão original de quebra de linha (`LF` ou `CRLF`).

### 💻 Gerador de Escapes para Código

Gera e copia com 1 clique representações prontas para colar no código-fonte:

* **JavaScript / JSON:** `\uXXXX` e formato moderno ES6 `\u{XXXXX}` para emojis suplementares.

* **UTF-8 Hex Literal:** `\xXX` compatível com C, Python e buffers binários.

* **HTML Entities:** `&#xXXXX;` escapando caracteres não-ASCII e símbolos reservados HTML.

* **URL Percent-Encoding:** `%XX` para transporte seguro em *query strings*.

### 📂 Importação, Exportação e Privacidade

* **Detecção Automática de BOM:** Suporta importação via seletor ou *Drag & Drop* com detecção automática de assinaturas **UTF-8** (`EF BB BF`), **UTF-16 LE** (`FF FE`) e **UTF-16 BE** (`FE FF`).

* **Exportação Versátil:** Baixe o resultado limpo em **`.TXT` (UTF-8)** ou gere um relatório completo em **`.JSON`** contendo todos os diagnósticos e escapes.

* **Privacidade Total (Zero-Backend):** Todo o processamento ocorre na memória do navegador (`TextEncoder`, `TextDecoder`, `String.prototype.normalize`). Nenhum dado é enviado para servidores externos.

## 🚀 Como Usar

Por ser construído em arquitetura **Single-File** (`appUnicodeInspector.html`), não requer instalação de Node.js, bundlers ou dependências:

1. **Clone o repositório:**

   ```
   git clone https://github.com/seu-usuario/unicode-mojibake-inspector.git
   
   ```

2. **Execute localmente:**
   Abra o arquivo `appUnicodeInspector.html` diretamente em qualquer navegador moderno (Chrome, Firefox, Edge, Safari) ou publique via **GitHub Pages**, **Vercel** ou **Netlify**.

## 🧩 Suíte Integrada com o Byte Counter

Este aplicativo foi projetado para trabalhar em conjunto com o **Byte Counter** (`appByteCalc.html`):

* Compartilha a mesma identidade visual (**Amber & Teal Edition**) e sincroniza automaticamente a preferência de **Tema Claro / Escuro** via `localStorage`.

* Enquanto o **Byte Counter** mede o peso exato em bytes, escalas (`KB`/`MB`/`GB`) e payloads Base64, o **Unicode & Mojibake Inspector** diagnostica e corrige a estrutura interna dos caracteres.

## ⌨️ Atalhos e Controles

| Atalho / Ação | Descrição | 
| ----- | ----- | 
| `Ctrl / Cmd + Enter` | Força a reinspeção imediata de todo o texto | 
| **Amostras de Bugs** | Carrega exemplos reais (*Mojibake*, *Zero-Width/NBSP*, *NFD vs NFC*, *Emoji ZWJ*) | 
| **Mostrar espaços/quebras** | Alterna a exibição visual de espaços (`·`), `→TAB`, `↵LF` e `⏎CR` na Visão Raio-X | 
| **Alternar Tema** | Alterna entre o modo escuro (`#0A0D14`) e o modo claro fosco de baixo reflexo | 

## 📄 Licença

Distribuído sob a licença **MIT**. Sinta-se livre para usar, adaptar e integrar ao seu fluxo de desenvolvimento.
