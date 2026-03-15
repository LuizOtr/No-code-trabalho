# Documentação Técnica — App Bíblico (Glide)

**Atualizado em:** 15/03/2026

## 1. Estrutura de Banco de Dados

O banco de dados foi otimizado para respeitar as limitações do plano gratuito do Glide (evitando estourar o limite de linhas), consolidando dados de forma inteligente.

### Tabela: `user`
Gerencia os dados e permissões de acesso.
* **nome:** Texto
* **email:** E-mail
* **foto:** Imagem
* **tipo_regra:** Texto (Define papéis e permissões — *Pendente de configuração*)

### Tabelas de Planos (`plano_365`, `plano_90`, `plano_30`)
Gerencia as metas de leitura do usuário. O formato é replicado para os três ritmos de leitura.
* **dia:** Número (ex: Dia 1, Dia 2)
* **referencia:** Texto (ex: Gênesis 1 a 3)
* **texto_completo:** Texto Longo (O conteúdo exato que deve ser lido na meta do dia)
* **status:** Escolha/Choice (Opções: `Pendente`, `Em andamento`, `Concluído`). Status mutável pelo usuário.

### Tabela: `biblia_por_capitulo`
Base principal de leitura estruturada para economia de linhas.
* **livro:** Texto (ex: Gênesis)
* **capitulo:** Número (ex: 1)
* **versiculos:** Texto Longo (Contém todos os versículos do capítulo agrupados).
> **Nota de Arquitetura:** O agrupamento por capítulo (ex: Gênesis 2, versículos 1 a 25 consolidados) é uma solução arquitetural para não exceder a cota de linhas do plano free do Glide, mantendo o banco leve e funcional, mesmo para livros longos como Salmos.

---

## 2. Diretrizes de UI/UX e Acessibilidade (IxD)

A interface deve seguir rigorosamente o Guia de Identidade Visual, adaptando-se às limitações visuais do Glide, mas preservando a essência inclusiva.

* **Acessibilidade e Inclusão (Cores Sensíveis):** Implementação obrigatória do Modo Noturno (fundo `#12151A` e textos claros) para usuários com sensibilidade à luz (fotofobia). As cores passaram por validação de contraste WCAG AA.
* **Paleta Principal (Modo Claro):** * Fundo de leitura: Pergaminho (`#F7F4EE`) para conforto visual.
  * Ações primárias: Azul Profundo (`#1B3F6B`).
  * Destaques: Dourado Âmbar (`#C9972A`).
* **Tipografia:** * *Lora* (Serifada) para títulos, cabeçalhos e versículos em destaque.
  * *Nunito* (Sem serifa) para o texto corrido (leitura principal), botões e navegação, garantindo máxima legibilidade.

---

## 3. Backlog e Próximos Passos (Pendências)

* [ ] **Tela de Pesquisa:** Finalizar a prototipação da interface e integrar a barra de busca no Glide (apontando para a tabela `biblia_por_capitulo`).
* [ ] **Roles/Regras de Usuário:** Configurar a lógica de visibilidade no Glide baseada na coluna `tipo_regra` da tabela de usuários.
* [ ] **Ajuste de Tema:** Garantir que o Glide alterne corretamente as cores do Guia Visual ao mudar do modo claro para o escuro nas configurações do sistema/app.