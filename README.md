# ⚡ PRAETORIAN FINANCIAL NETWORK v3.17

Uma aplicação web de controle financeiro pessoal com uma estética retro-futurista inspirada nos terminais CRT de fósforo verde (estilo *cyberpunk / Tron / Matrix*). O sistema é totalmente funcional, integrado ao **Supabase** para persistência de dados, autenticação de usuários e geração de relatórios consolidados para impressão.

---

## 🚀 Funcionalidades

- **Autenticação Segura:** Sistema de login integrado ao Supabase Auth.
- **Gerenciamento de Transações:** Registro dinâmico de receitas e despesas com categorização inteligente.
- **Filtros Avançados de Linha do Tempo:** Filtragem por histórico completo, anos consolidados ou meses específicos para evitar sobrecarga de dados.
- **Meters de Gasto:** Gráficos de barra nativos (utilizando a tag HTML `<progress>`) baseados na distribuição percentual das despesas.
- **Engine de Impressão:** Folha de estilos `@media print` otimizada para gerar relatórios financeiros limpos, legíveis e minimalistas em papel ou PDF.
- **Easter Egg:** Um aceno clássico ao filme *The Net (1995)* embutido na interface.

---

## 🛠️ Tecnologias Utilizadas

- **Frontend:** HTML5, CSS3 (Variáveis CSS, CSS Grid, Flexbox) e JavaScript Vanilla (ES6+).
- **Backend as a Service (BaaS):** [Supabase](https://supabase.com/) (PostgreSQL Database & Auth).
- **Icons/Fonts:** Monospace standard rendering (`Courier New`).

---

## 📦 Como Instalar e Rodar o Projeto

1. **Clone o repositório:**
   ```bash
   git clone [https://github.com/seu-usuario/praetorian-financial.git](https://github.com/seu-usuario/praetorian-financial.git)

---

## 💾 Configure o Banco de Dados (Supabase):

No editor SQL do seu painel do Supabase, execute o seguinte script para provisionar a tabela necessária:

  '''create table lancamentos (
    id uuid default gen_random_uuid() primary key,
    user_id uuid references auth.users not null, -- Vincula o gasto ao usuário logado
    tipo text not null, -- 'receita' ou 'despesa'
    valor numeric not null,
    categoria text not null,
    descricao text,
    created_at timestamp with time zone default timezone('utc'::text, now()) not null
  );
  
  -- Ativar Row Level Security (Segurança para um usuário não ver os dados do outro)
  alter table lancamentos enable row level security;
  
  -- Criar a política que permite usuários lerem/escreverem apenas seus próprios dados
  create policy "Usuários podem gerenciar seus próprios lançamentos" 
  on lancamentos for all 
  using (auth.uid() = user_id);'''

---

## 🔐 Insira as credenciais:
Abra o arquivo index.html e substitua as constantes pelas chaves do seu projeto:

  '''const SUPABASE_URL = "SUA_URL_DO_SUPABASE";
  const SUPABASE_ANON_KEY = "SUA_CHAVE_ANON_DO_SUPABASE";'''
