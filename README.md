# Quadro PCP

Kanban de post-its animados para deixar tarefas e responder dentro de cada uma.
Site estático (HTML + JS puro) com Supabase para login, banco e tempo real; publicado na Vercel.

## Como funciona

- **Raias:** A fazer, Fazendo, Aguardando resposta, Feito.
- **Post-it:** título, detalhes, prazo, cor, responsável. Arraste entre raias (no celular, segure antes de arrastar ou use "Mover para").
- **Respostas:** abra o post-it para conversar; o contador é mantido pelo banco.
- **Login:** e-mail e senha (Supabase Auth). Só quem está logado vê e edita o quadro.

## Arquivos

| Arquivo | O que é |
|---|---|
| `index.html` | O app inteiro (estilos, interface e lógica) |
| `config.js` | URL do Supabase e chave pública (publishable) |

## Banco (Supabase)

Tabelas no schema `public`, todas com RLS:

- `quadro_membros` — nome de cada usuário (id = `auth.users.id`)
- `quadro_tarefas` — os post-its
- `quadro_respostas` — respostas de cada post-it (trigger atualiza `quadro_tarefas.respostas`)

Regras: usuários logados leem tudo, criam em seu próprio nome, editam e apagam post-its; cada um apaga só as próprias respostas. Visitantes sem login não acessam nada.

## Rodar localmente

Qualquer servidor estático serve, por exemplo:

```bash
npx serve .
```

Para os links de confirmação e de recuperação de senha voltarem para o site certo, adicione a URL do site em
Supabase → Authentication → URL Configuration (Site URL e Redirect URLs).
