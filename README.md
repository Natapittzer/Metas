# Controle de Metas 💰🎯

Aplicação em HTML/CSS/JS para registrar vendas diárias, acompanhar meta mensal, visualizar gráficos e **sincronizar dados com Firebase** (login + Firestore).

---

## ✅ Principais recursos

### 📥 Vendas / Registros
- Adicionar venda por **data + valor** com validações:
  - bloqueia **data futura**
  - bloqueia **valor zero/negativo**
- **Detecção de duplicatas** (mesma data):
  - opção de **somar** ou **substituir** o valor
- **Editar venda** (modal)
- **Excluir venda** (com confirmação)
- **Busca/filtro** na tabela por data/valor

### 📊 Resumo e Estatísticas
- Resumo mensal: **Total do Mês**, **Meta**, **Faltam**
- Barra de progresso com **% exibida**
- Estatísticas extras:
  - **Média diária**
  - **Dias trabalhados**
  - **Melhor dia**
  - **Menor dia**
- **Previsão para bater a meta**:
  - dias restantes no mês
  - valor necessário por dia

### 📈 Gráficos
- Gráfico **Vendas do Mês** (linha)
- Gráfico **Comparativo últimos 30 dias** (barras: período anterior vs atual)
- Botão para **mostrar/esconder gráficos** (salva preferência)
- Exportação de gráficos em **PNG**

### 💾 Backup / Importação
- Exporta dados em:
  - **JSON** (backup completo)
  - **CSV**
- Importa dados:
  - JSON (substitui tudo)
  - CSV (adiciona aos dados existentes)

### 🎨 Aparência
- **Modo escuro** (persistente)
- **Imagem de fundo personalizada** (com opção de remover)
- **Notificações Toast** (sucesso/erro/aviso/info)

### 🧹 Manutenção de dados
- **Limpar Dados** (apaga tudo)
- **Limpar Mês** (apaga todas as vendas do mês selecionado)

---

## 🆕 Updates recentes (Release Notes)

- ✅ **Tags/Categorias** nas vendas (ex: Loja, Online, Indicação)
- ✅ **Relatório PDF**: meta + total batido + gráficos
- ✅ **Login + Sincronização** com Firebase (Auth + Firestore)
- ✅ Regras/ajustes para permitir **compartilhamento entre PCs** via nuvem
- ✅ Melhorias de UX: toasts, modais, validações e layout responsivo

---

## 🚀 Publicar no GitHub (GitHub Pages)

### Vai funcionar no GitHub Pages?
✅ Sim — desde que você publique em **HTTPS** (GitHub Pages já é https) e autorize o domínio no Firebase.

### Passo a passo (bem rápido)
1. Suba o projeto para um repositório no GitHub.
2. Ative o GitHub Pages:
   - Repo → **Settings** → **Pages**
   - Source: `main` (ou branch correta) e pasta `/root` (ou `/docs`)
3. Copie a URL gerada (ex: `https://seuusuario.github.io/seurepo/`)

---

## 🔥 Firebase (Login + Firestore) — Configuração

### 1) Pegar o firebaseConfig (inclui apiKey)
No Firebase Console:
- Projeto → ⚙️ **Configurações do projeto**
- Em **Seus aplicativos**, crie/registre um **App Web** (ícone `</>`)
- Ele vai mostrar um bloco com:

```js
const firebaseConfig = {
  apiKey: "...",
  authDomain: "...",
  projectId: "...",
  storageBucket: "...",
  messagingSenderId: "...",
  appId: "..."
};
```

✅ Você usa **tudo** desse objeto (apiKey + campos abaixo).

> Observação: a `apiKey` pode ficar no front-end. O que protege seus dados são as **Firestore Rules**.

### 2) Ativar o provedor de Login
Firebase Console → **Authentication** → **Sign-in method**
- Ative **Email/Password** (ou o provedor que você estiver usando)

> Se aparecer erro `auth/operation-not-allowed`, é porque o provedor ainda não foi ativado.

### 3) Autorizar domínio do GitHub Pages
Firebase Console → **Authentication** → **Settings** → **Authorized domains**
- Adicione:
  - `seuusuario.github.io`
- Se você usa um domínio próprio, adicione também.

### 4) Firestore: precisa criar coleção manualmente?
➡️ **Não é obrigatório**. O Firestore cria automaticamente quando seu app gravar o primeiro documento.

Se quiser criar manualmente:
- Firestore Database → **Dados** → **Iniciar coleção**
- Sugestão de nome: `users`

### 5) Regras do Firestore (importante)
Para sincronização por usuário (cada um vê apenas seus dados), use regras assim:

```js
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {

    // Cada usuário pode ler/escrever apenas no próprio documento
    match /users/{userId} {
      allow read, write: if request.auth != null && request.auth.uid == userId;
    }

  }
}
```

Depois clique em **Publicar**.

---

## ✅ Checklist pós-publicação
- [ ] Site abrindo em `https://seuusuario.github.io/...`
- [ ] `seuusuario.github.io` em **Authorized domains**
- [ ] **Email/Password** (ou provedor) ativado no Auth
- [ ] Regras do Firestore publicadas
- [ ] Após logar, os dados aparecem em outro PC

---

## 🧩 Tecnologias
- HTML + CSS + JavaScript
- Chart.js (gráficos)
- canvas-confetti (efeito ao bater meta)
- Firebase Auth + Firestore (sincronização)

---

## 📝 Licença
Use como quiser no seu projeto. Se publicar, uma menção/credito é bem-vindo 🙂
