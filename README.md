#  O Atividade Forense de Hash — SHA-256 no Windows 11

## Objetivo

Nesta atividade vais participar num pequeno desafio de **integridade digital**.

Será apresentada à turma durante **10 minutos**. Depois, a mensagem é transmitida e um dos participantes poderá introduzir uma alteração. No final, outro participante terá de analisar a mensagem e descobrir, através do **SHA-256**, se o conteúdo foi alterado.

> **Regra de ouro:** uma alteração mínima no ficheiro ou no texto produz, normalmente, um hash completamente diferente.

---

# ⚽ Texto 1 — FC Porto 3-1 Benfica

O FC Porto recebeu o Benfica no Estádio do Dragão num jogo de grande intensidade.  
A equipa azul e branca conseguiu marcar três golos durante a partida.  
O Benfica ainda reduziu a diferença, mas não conseguiu evitar a derrota por 3-1.  
No final, o FC Porto celebrou uma vitória perante os seus adeptos.

> **Referência factual:** FC Porto 3-1 Benfica, 20 de setembro de 2026, Estádio do Dragão.

---

# 🇵🇹 Texto 2 — Portugal frente a Espanha no Mundial

Portugal encontrou a Espanha nos oitavos de final do Mundial de 2026.  
A partida foi equilibrada durante grande parte do encontro.  
A Espanha marcou já perto do final e conseguiu vencer por 1-0.  
Portugal ficou assim eliminado depois de uma partida decidida nos últimos minutos.

> **Referência factual:** Portugal 0-1 Espanha, 6 de julho de 2026, oitavos de final do Mundial de 2026.

---

# 🏎️ Texto 3 — Fórmula 1: Max, Lewis e Kimi

Em 2024, Max Verstappen e Lewis Hamilton continuaram a protagonizar momentos importantes na Fórmula 1.  
No Grande Prémio da Grã-Bretanha de 2024, Hamilton venceu e Verstappen terminou em segundo.  
Em 2026, Kimi Antonelli passou a estar na luta pelo topo e chegou a liderar o campeonato.  
No Grande Prémio do Canadá de 2026, Kimi venceu, com Lewis Hamilton em segundo e Max Verstappen em terceiro.

> **Referência factual:** no GP do Canadá de 2026, Antonelli terminou em 1.º, Hamilton em 2.º e Verstappen em 3.º. À data desta atividade, Antonelli lidera o campeonato de pilotos de 2026.

---

# 🖥️ O Teste Forense de Hash no Windows 11

## 1. Abrir o Terminal

Clica com o botão direito do rato no **menu Iniciar** do Windows e escolhe:

**Terminal**

Também podes procurar por **PowerShell** na barra de pesquisa do Windows.

---

## 2. Criar o ficheiro com a prova

Primeiro, vamos criar um ficheiro de texto que contém a mensagem.

No PowerShell, escreve:

```powershell
Set-Content -Path .\caso_sha256.txt -Value "O FC Porto venceu o Benfica por 3-1 no Estádio do Dragão."
```

Carrega em **Enter**.

Foi criado um ficheiro chamado:

```text
caso_sha256.txt
```

---

# 🔐 3. Gerar o SHA-256

Agora vamos calcular o hash do ficheiro.

Executa:

```powershell
Get-FileHash .\caso_sha256.txt -Algorithm SHA256
```

O PowerShell vai apresentar algo semelhante a:

```text
Algorithm       Hash                                                                   Path
---------       ----                                                                   ----
SHA256          7A8F...                                                                C:\...\caso_sha256.txt
```

O valor enorme constituído por letras e números é o **SHA-256** do ficheiro.

⚠️ **Não compares apenas os primeiros caracteres. Para uma verificação correta, compara o hash completo.**

---

# 🚨 4. O Teste da Adulteração

Agora vamos fazer aquilo que acontece no desafio.

Altera o conteúdo do ficheiro:

```powershell
Set-Content -Path .\caso_sha256.txt -Value "O FC Porto venceu o Benfica por 2-1 no Estádio do Dragão."
```

Repara que apenas alterámos **3 para 2**.

Agora calcula novamente:

```powershell
Get-FileHash .\caso_sha256.txt -Algorithm SHA256
```

O hash será diferente.

Mesmo uma alteração muito pequena no conteúdo faz com que o resultado SHA-256 deixe de corresponder ao hash anterior.

---

# 🕵️ 5. O Desafio Forense

Agora começa o jogo.

### Participante A — O Leitor

Recebe o texto e tem **10 minutos** para o ler e memorizar.

### Participante B — O Alterador

Recebe a mensagem e altera uma parte dela.

Pode alterar:

- uma palavra;
- um número;
- uma pontuação;
- uma frase;
- uma letra;
- ou outro pequeno detalhe definido pelo professor.

**Não pode revelar o que alterou.**

### Participante C — O Investigador

Recebe a versão final e calcula o SHA-256.

O seu objetivo é determinar se a mensagem é exatamente a mesma que a original.

---

# 🏆 Sistema de Pontuação

| Situação | Pontos |
|---|---:|
| Investigador deteta corretamente que houve alteração | +1 Investigador |
| Investigador não deteta a alteração | +1 Alterador |
| Alteração é descoberta através da comparação dos hashes | +1 Investigador |
| Alterador consegue passar despercebido | +1 Alterador |

O professor pode aumentar a dificuldade em cada ronda.

### Ronda fácil
Alterar uma palavra evidente.

### Ronda média
Alterar apenas um número ou uma pequena expressão.

### Ronda difícil
Alterar apenas uma letra, espaço ou sinal de pontuação.

---

# 🧠 O que estamos realmente a aprender?

O SHA-256 funciona como uma **impressão digital digital do conteúdo**.

Não é necessário ler o ficheiro inteiro para perceber que alguma coisa mudou: se o ficheiro original e o ficheiro recebido produzirem hashes diferentes, sabemos que os conteúdos **não são idênticos**.

Por exemplo:

```text
Mensagem original
        ↓
     SHA-256
        ↓
HASH A
```

Depois de uma alteração:

```text
Mensagem alterada
        ↓
     SHA-256
        ↓
HASH B
```

Se:

```text
HASH A ≠ HASH B
```

então os ficheiros não são iguais.

---

# ⚠️ Importante

O SHA-256 permite verificar a **integridade** de um conteúdo, mas não diz, por si só:

- quem alterou o ficheiro;
- quando ocorreu a alteração;
- qual foi a alteração;
- se determinada pessoa é responsável pela alteração.

O hash serve para comparar o estado do conteúdo. A identificação de quem o alterou exige outros elementos de prova e registos.

---

# 🎮 Desafio final

No final da atividade, o professor entrega uma mensagem aparentemente igual à original.

Tens de:

1. receber o ficheiro;
2. calcular o SHA-256;
3. comparar com o hash original;
4. decidir se houve alteração;
5. explicar como chegaste à conclusão.

**Atenção:** não basta dizer que “parece igual”.

No mundo digital, uma alteração pode estar escondida à vista de todos.

---

## 📚 Fontes

- Formula 1 — resultados oficiais de 2024 e 2026.
- FIFA — Portugal vs. Espanha, Mundial de 2026.
- ZeroZero — FC Porto 3-1 Benfica, 20 de setembro de 2026.
