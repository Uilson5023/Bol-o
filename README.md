# Bolão Copa do Mundo 2026 — Sistema Web

Sistema completo (Python + Flask + SQLite) baseado na sua planilha
"Bolão Copa do Mundo 26", com:

- ✅ Cadastro e login de apostadores
- ✅ Tela para cada usuário inserir seus palpites nos 72 jogos da fase de grupos
  (os confrontos já vêm pré-carregados a partir da sua planilha, incluindo os
  resultados que já estavam preenchidos)
- ✅ Área do organizador (admin) para lançar/corrigir o resultado de cada partida
- ✅ Cálculo automático da pontuação de cada palpite, seguindo exatamente as
  regras da aba "Regras" da sua planilha:
    - 10 pts → placar exato
    - 6 pts  → vencedor (ou empate) + nº de gols de uma das seleções
    - 4 pts  → somente o vencedor
    - 4 pts  → empate "não exato" (acertou que seria empate, mas não o placar)
    - 1 pt   → número de gols de apenas uma das seleções
    - 0 pts  → não acertou nada
- ✅ Ranking geral, atualizado automaticamente sempre que um resultado é lançado

## Como executar

1. Tenha o Python 3.10+ instalado.
2. Instale a dependência (apenas o Flask é necessário):
   ```bash
   pip install flask
   ```
3. Dentro da pasta do projeto, rode:
   ```bash
   python app.py
   ```
4. Acesse **http://localhost:5000** no navegador.

O banco de dados (`bolao.db`) é criado automaticamente na primeira execução,
já populado com os 72 jogos extraídos da sua planilha (com os placares que já
estavam lançados nela).

## Login do organizador (admin)

Um usuário organizador é criado automaticamente:

- **E-mail:** admin@bolao.com
- **Senha:** admin123

Recomendo trocar essa senha depois (ou simplesmente criar um novo usuário
admin direto no banco e remover esse).

Com esse login, vai aparecer no menu a opção **"Lançar Resultados"**, onde
você atualiza o placar real de qualquer jogo. Ao salvar, o sistema recalcula
automaticamente a pontuação de todos os apostadores que palpitaram naquele
jogo, e o ranking já aparece atualizado na página inicial.

## Cada apostador

1. Cria a própria conta em "Cadastrar".
2. Faz login.
3. Vai em "Meus Palpites" e preenche o placar que imagina para cada jogo
   ainda não realizado (jogos já finalizados aparecem bloqueados, mostrando
   o palpite enviado e os pontos ganhos).
4. Acompanha sua posição em "Ranking".

## Estrutura de arquivos

```
bolao/
├── app.py              # aplicação Flask (toda a lógica do sistema)
├── games.json           # os 72 jogos extraídos da sua planilha original
├── bolao.db              # banco de dados SQLite (criado automaticamente)
└── templates/
    ├── base.html
    ├── login.html
    ├── cadastro.html
    ├── palpites.html
    ├── ranking.html
    └── admin_resultados.html
```

## Observações / próximos passos possíveis

- Hoje o sistema trava a edição do palpite apenas quando o **resultado já foi
  lançado** (e não por data/hora do jogo). Se você quiser bloquear pelo
  horário real de início de cada partida, é só me avisar que adiciono um
  campo de data/hora para cada jogo.
- Para publicar isso na internet (e não só rodar localmente), o app pode ser
  hospedado em serviços como Render, Railway, PythonAnywhere etc. — também
  posso ajudar a preparar isso, se quiser.
- O critério de desempate da planilha original (maior número de placares
  exatos, depois vencedor+gols, etc.) já está refletido na ordenação do
  ranking.
