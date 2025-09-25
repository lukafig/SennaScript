# APS — Lógica da Computação 2025/2  
# SennaScript

###  Objetivo
Definir formalmente a linguagem **SennaScript** em **EBNF (Extended Backus–Naur Form)**.  
A SennaScript é uma linguagem de alto nível inspirada no automobilismo, projetada para controlar um carro em uma pista simulada.  

---

###  Descrição da Linguagem
A **SennaScript** oferece:  
- **Declarações de variáveis** (`var pos = 0;`).  
- **Sensores somente leitura**:  
  - `fuel` → nível de combustível.  
  - `lap` → volta atual.  
  - `pos` → posição atual.  
- **Ações**:  
  - `acelerar;`  
  - `frear;`  
  - `mover;`  
- **Estruturas de controle**:  
  - `se (...) { ... } [ senao { ... } ]`  
  - `enquanto (...) { ... }`  
- **Saída**: `escrever(...)`.  

---
###  Palavras-reservadas

| Palavra     | Função                                                                 |
|-------------|------------------------------------------------------------------------|
| **corrida** | Define o início do programa principal.                                 |
| **var**     | Declara uma variável inteira.                                          |
| **se**      | Estrutura condicional (if).                                            |
| **senao**   | Bloco alternativo da condição (else).                                  |
| **enquanto**| Estrutura de repetição (while).                                        |
| **escrever**| Exibe valores (variáveis, sensores ou expressões).                     |
| **acelerar**| Aumenta a velocidade do carro.                                         |
| **frear**   | Diminui a velocidade do carro.                                         |
| **mover**   | Atualiza a posição do carro de acordo com a velocidade atual.          |
| **fuel**    | Sensor: nível de combustível restante (somente leitura).               |
| **lap**     | Sensor: volta atual do carro (somente leitura).                        |
| **pos**     | Sensor: posição atual do carro na pista (somente leitura).             |


###  Definição Formal (EBNF)

```ebnf
(* Programa principal *)
programa   = "corrida", "{", { declaracao | comando }, "}" ;

(* Declarações de variáveis *)
declaracao = "var", identificador, "=", expressao, ";" ;

(* Comandos possíveis *)
comando    = atribuicao | condicional | loop | escrita | acao ;

(* Atribuição *)
atribuicao = identificador, "=", expressao, ";" ;

(* Condicional if/else *)
condicional = "se", "(", expressao, ")", bloco, [ "senao", bloco ] ;

(* Estrutura de repetição while *)
loop       = "enquanto", "(", expressao, ")", bloco ;

(* Saída de dados *)
escrita    = "escrever", "(", expressao, ")", ";" ;

(* Ações específicas do carro *)
acao       = "acelerar" ";" 
           | "frear" ";" 
           | "mover" ";" ;

(* Blocos de comandos *)
bloco      = "{", { comando }, "}" ;

(* Expressões aritméticas e relacionais *)
expressao  = termo, { ("+" | "-" | ">" | "<" | "==" | ">=" | "<="), termo } ;

termo      = fator, { ("*" | "/"), fator } ;

fator      = numero | identificador | sensor | "(", expressao, ")" ;

(* Sensores disponíveis (somente leitura) *)
sensor     = "fuel" | "lap" | "pos" ;

(* Tokens básicos *)
identificador = letra, { letra | digito | "_" } ;

numero     = digito, { digito } ;

letra      = "a" | ... | "z" | "A" | ... | "Z" ;

digito     = "0" | ... | "9" ;
```

---

###  Exemplos em **SennaScript**

#### Exemplo 1 — Corrida simples
```txt
corrida {
    var pos = 0;
    var v = 1;

    escrever(pos);
    acelerar;
    mover;
    escrever(pos);
}
```

#### Exemplo 2 — Loop com sensor de combustível
```txt
corrida {
    var pos = 0;

    enquanto (fuel > 0) {
        mover;
        se (pos > 100) {
            frear;
        }
        escrever(pos);
    }
}
```

