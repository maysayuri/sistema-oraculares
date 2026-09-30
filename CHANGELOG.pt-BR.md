# CHANGELOG

Todas as alterações relevantes deste projeto estão documentadas neste arquivo.  
O projeto adota um modelo de versionamento progressivo alinhado aos marcos de entrega de funcionalidades.

---

## [v8.0] - 2024 - Otimização para Desktop & Sistema de Layout Adaptativo

### Adicionado
- Layout desktop completo para telas ≥ 1024px, implementado inteiramente via CSS sem modificar lógica JavaScript ou estrutura DOM.
- Sistema responsivo de três breakpoints: `768px` (tablet paisagem), `1024px` (desktop), `1600px` (telas grandes) - sobreposto à fundação mobile-first existente sem alterá-la.
- Layout CSS Grid multicolunas em ≥ 1024px organizando o conteúdo em: coluna de navegação / área de grid de cartas / painel de análise.
- Estados de hover para todos os componentes de carta interativos: `spec-card`, `arcano-card`, `wm-card`, `n52-carta`, `tir-card` - cada um com elevação via `translateY` e profundidade por `box-shadow` ao posicionar o cursor.
- Estilização de scrollbar customizada (`::webkit-scrollbar`) com thumb na cor da identidade visual e track minimalista.
- Escala tipográfica fluida via `clamp()` nos títulos principais (`eb-h1`, `portal-h1`), prevenindo overflow em viewports extremas.

### Melhorado
- Barra de navegação por abas (`eb-nav`) promovida a `position: sticky` com `backdrop-filter: blur(12px)` - permanece ancorada ao topo do viewport durante rolagem vertical, eliminando a necessidade de retornar ao início para navegar entre abas em conteúdos longos.
- Botão voltar (`btn-voltar`) reposicionado para `position: fixed` no canto superior esquerdo do viewport em ≥ 1024px, sempre acessível independente da profundidade de rolagem.
- Grids de cartas (`arcanos-grade`, `wm-grid`, `tir-grid`) expandidos para três colunas via `repeat(auto-fill, minmax(300px, 1fr))`, proporcionando melhor densidade visual e equilíbrio espacial em telas largas.
- Grid de cartas dos baralhos específicos (`spec-grade`) expandido para duas colunas largas via `minmax(480px, 1fr)`, melhorando a legibilidade do conteúdo extenso das cartas.
- Grid de resoluções (`res-naipe-lista`) reorganizado em duas colunas em ≥ 1024px, reduzindo o excesso de rolagem vertical.
- Altura das ilustrações aumentada: `arcano-img-wrap` de 180px para 220px, `wm-img-wrap` de 155px para 260px - proporcional à maior área das cartas em larguras desktop.
- Modal de carta individual (`sim-modal-card`) com padding de `2.5rem 3rem` e `max-width` limitado a `780px` para comprimento de linha confortável.
- Seção LUZ/SOMBRA do modal (`sim-modal-luz-sombra`) renderizada em duas colunas; seção Passado/Presente/Futuro (`sim-modal-ppf`) em três colunas - eliminando o empilhamento em coluna única em telas grandes.
- Painel de análise da leitura completa (`slg-ppf`) renderizado como grid de 3 colunas em ≥ 1024px, alinhando cada posição temporal lado a lado.
- Containers de conteúdo (`eb-wrap`, `sim-topo`) limitados a `max-width: 1400px` e centralizados com `margin: 0 auto`, prevenindo esticamento em monitores ultra-wide.
- Em ≥ 1600px, `eb-wrap` expande para `max-width: 1500px` e grids de cartas escalam para `minmax(320px, 1fr)`, mantendo densidade proporcional sem esticar excessivamente.

### Técnico
- Todas as regras desktop estão isoladas em blocos `@media (min-width: ...)` adicionados ao final da stylesheet - zero interferência com as 14 queries `max-width` de ajuste mobile existentes.
- A implementação sticky da barra de abas utiliza compensação de `margin-left`/`margin-right` negativo (`-3rem`) com `padding-left`/`padding-right` correspondente, permitindo que a barra ocupe a largura total do container sem expandir o próprio container.
- `backdrop-filter` e `-webkit-backdrop-filter` aplicados em conjunto para compatibilidade cross-browser na nav sticky e no botão fixo.

---

## [v7.0] - 2024 - Consolidação de Identidade e Padronização de Nomenclatura

### Alterado
- Substituição dos títulos genéricos de tiragens nos três sistemas de entidade por nomes próprios que refletem a identidade cultural e espiritual de cada entidade, estabelecendo um padrão de nomenclatura consistente em toda a plataforma.

**Malandragem - Zé Pelintra:**
| Anterior | Atual |
|---|---|
| A Jogada Simples | O Chapéu do Malandro |
| A Encruzilhada | Os 3 Saravá |
| O Jogo do Malandro | Os Arcos da Lapa |
| O Baralho do Zé | As 7 Navalhas |
| A Mesa do Malandro | A Mesa do Malandro *(mantido)* |
| O Reinado do Zé | Ginga da Malandragem |

**Pomba Gira 7 Rosas:**
| Anterior | Atual |
|---|---|
| A Pergunta da Rainha | Gargalhada da Moça |
| O Triângulo do Fogo | As 3 Rosas Vermelhas |
| A Cruz da Calunga | A Cruz da Calunga *(mantido)* |
| O Altar da Rosa | As 7 Rosas |
| Os Sete Véus | Fios de Conta |
| O Ano da Rosa | Pétalas da Roseira |

**Exu Tatá Caveira:**
| Anterior | Atual |
|---|---|
| O Veredito | O Trono do Tatá |
| A Cruz Mestra | A Cruz do Cruzeiro |
| As Cinco Cruzes | Jogo dos Ossos |
| Os Sete da Calunga | O Sete da Calunga *(mantido)* |
| A Revelação da Cruz | A Revelação das 9 Covas |
| O Ciclo da Calunga | O Ciclo da Calunga *(mantido)* |

---

## [v6.0] - 2024 - Camada Visual: Arcanos Menores

### Adicionado
- Renderização de ilustrações em resolução completa do Rider-Waite em cada um dos 56 cards dos Arcanos Menores, utilizando arte original de domínio público proveniente de *The Pictorial Key to the Tarot*.

### Corrigido
- Resolvido conflito de `z-index` entre o elemento placeholder do card e a ilustração carregada, que anteriormente causava sobreposição do placeholder sobre a imagem em browsers mobile.

### Refatorado
- Unificado e desduplicado o conjunto de regras CSS para `.wm-img-wrap`, `.wm-img`, `.wm-img-ph` e `.wm-img-overlay` - eliminadas três declarações conflitantes acumuladas em ciclos iterativos de desenvolvimento.
- Aplicado `object-fit: contain` às imagens dos cards, garantindo visibilidade completa da carta sem recorte, consistente com o comportamento de renderização dos Arcanos Maiores.

---

## [v5.0] - 2024 - Integridade Estrutural e Estabilidade de Navegação

### Corrigido
- Resolvido desequilíbrio crítico na estrutura HTML causado por aninhamento incorreto de `<div>` nas seções de múltiplas entidades (`mal`, `ros`, `cav`, `wai`). O desequilíbrio causava interpretação equivocada do DOM, renderizando conteúdo de abas fora do elemento pai e tornando-o inacessível via seletores CSS utilizados por `trocarTab()`.
- Corrigida a profundidade de aninhamento dos elementos `sim-overlay` e `sim-tutorial`, que estavam sendo renderizados dentro do container `eb-wai` em vez de no nível raiz - impedindo a inicialização correta do jogo interativo.
- Restaurada a visibilidade das abas Tiragens e Resoluções em todos os três sistemas de entidade (`mal-tir`, `mal-res`, `ros-tir`, `ros-res`, `cav-tir`, `cav-res`).

### Refatorado
- Removidas as abas redundantes `wai-nai` (Ler com Naipes) e `wai-busca` (Busca) da navegação do Waite, consolidando a funcionalidade de busca na barra de busca global persistente já presente na interface.
- Renomeado o rótulo de navegação de `wai-tir` de "Como Jogar" para "Tiragens", corrigindo imprecisão semântica.

---

## [v4.0] - 2024 - Inteligência de Leitura e Refinamento de UX

### Adicionado
- Bloco **Conselho Lúcido** adicionado à análise de leitura completa (`fazerLeituraGeral`): agrega os campos `conselho_pratico` de todas as cartas reveladas em uma seção de orientação consolidada e orientada a ações concretas.
- Toggle colapsável (▲/▼) no bloco **Síntese Final** do painel de análise completa.
- Toggle colapsável (▲/▼) no bloco **Carta Invertida - como ler** dentro do modal individual de carta.

### Alterado
- Substituída a interpretação binária de carta invertida (troca automática luz/sombra) por um modelo de quatro perspectivas: **Bloqueio**, **Interiorização**, **Excesso**, **Ajuste** - eliminando o enquadramento negativo determinista e adotando uma abordagem contextual e não-fatalista.
- Atualizados os rótulos de carta invertida de "☽ ASPECTO SOMBRA (CARTA INVERTIDA)" para "☽ ASPECTO EM FOCO (INVERTIDA)", mantendo ambos os aspectos visíveis sem hierarquia de valor.

### Refatorado
- Normalizado o CSS de `slg-reflexao-txt`: removidos `font-style: italic` e `font-family: Playfair Display`, substituídos por `font-family: Inter` e `font-style: normal`, melhorando a legibilidade em telas mobile.
- Removido o rótulo redundante `✶ REFLEXÃO E CONSELHO` do modal individual - contexto já estabelecido pelo elemento de cabeçalho `CONSELHO`.

---

## [v3.0] - 2024 - Expansão de Conteúdo e Funcionalidades de Navegação

### Adicionado
- Integração das ilustrações originais do Rider-Waite para todas as 22 cartas dos Arcanos Maiores, renderizadas via componente `arcano-img-wrap` com overlay gradiente e badge posicional.
- Integração das ilustrações originais do Rider-Waite para todas as 56 cartas dos Arcanos Menores, com badge com código de cor por naipe.
- Barra de busca global (`filtrarWai78`) habilitando consulta entre seções em todas as 78 cartas do Tarot por nome, naipe ou número - com parser inteligente em português incluindo resolução de sinônimos (ex.: "ás" = "A", "valete" = "j" = "jota").
- Componente ibox colapsável (▲/▼) aplicado universalmente em todas as seções de conteúdo nos quatro sistemas.
- Cabeçalho contador `56 ARCANOS MENORES · 14 POR NAIPE` na aba `wai-men`, espelhando o contador dos Arcanos Maiores.
- Ibox "Cartas a Retirar" nas abas `spec/mm` e `cons` de cada sistema de entidade, especificando quais cartas remover do baralho de 52 antes de jogar.

### Alterado
- Padronizados os nomes das figuras nos Arcanos Menores, substituindo nomenclatura específica do sistema (Mensageiro, Guardiã, Mestre) pelos nomes canônicos: **Valete**, **Cavaleiro**, **Rainha**, **Rei**.
- Atualizados atributos `data-nome-alt` das figuras para incluir aliases de busca padrão.

### Corrigido
- Corrigido texto truncado no último `res-item` da aba Resoluções de cada entidade, que causava desequilíbrio de `</div>` e vazamento de conteúdo entre seções de ebook.

---

## [v2.0] - 2024 - Sistema de Consulta Interativa

### Adicionado
- **Jogo de consulta interativa** (`sim-overlay`): simulação completa de tiragem com animação de embaralhamento, mecânica de stop-to-select e sequência de revelação de cartas.
- **Análise de leitura completa** (`fazerLeituraGeral`): geração automatizada de painel completo incluindo detalhamento por carta, estatísticas da tiragem e Síntese Final.
- Sistema de cartas invertidas: probabilidade de 30% por carta sorteada, com indicador visual `↓` e enquadramento de leitura específico.
- Campo `conselho_pratico` renderizado por carta no modal individual e no painel de análise completa.
- Seis configurações de tiragem: 1, 3, 5, 7, 10 e 13 cartas, cada uma com layout posicional nomeado e rótulo descritivo.

### Alterado
- Extendido o modelo de dados JSON para todas as 78 cartas: `positivo`, `negativo`, `passado`, `presente`, `futuro`, `conselho`, `conselho_pratico`, `naipe_leitura`, `mesa_display`, `mesa_cor`.

---

## [v1.0] - 2024 - Lançamento Inicial

### Adicionado
- Aplicação web de arquivo único (HTML5 + CSS3 + JavaScript puro) sem dependências externas.
- Portal principal com quatro pontos de entrada: Malandragem, Pomba Gira 7 Rosas, Exu Tatá Caveira e Tarot Rider-Waite.
- Estrutura de ebook individual para cada um dos três sistemas de entidade, cada um contendo seis abas: Baralho Específico (36 cartas), Baralho de Consulta, Naipes 52 Cartas, Ler Sem o Baralho, Tiragens e Resoluções.
- Sistema Tarot Rider-Waite com quatro abas: Arcanos Maiores (22 cartas), Arcanos Menores (56 cartas), Tiragens e Resoluções.
- Função de navegação `trocarTab(eb, tab)` controlando visibilidade das abas via alternância de classe CSS (`.eb-tab.ativo`).
- Dataset JSON (`TODAS_CARTAS`) embutido inline com todas as 78 cartas do Tarot e metadados completos.
- 108 cartas autorais distribuídas pelos três sistemas de entidade (36 por sistema).
- 156 resoluções de naipes (52 por sistema), uma para cada carta do baralho padrão de 52.
- Sistema de correspondência de naipes mapeando ♦♥♠♣ para os campos espirituais de cada entidade.
- Layout responsivo mobile-first utilizando CSS Grid e Flexbox.
- Stack tipográfico: Playfair Display · Bebas Neue · Inter.

---

*Sistemas Oraculares - May Sayuri*  
*lumin.up07@gmail.com - [@ah.moncheri](https://instagram.com/ah.moncheri)*
