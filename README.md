# Trabalho_jogo_da_velha-

algoritmo "Jogo_da_Velha"

var
   tabuleiro: vetor[1..90] de caractere
   fechado: vetor[1..9] de logico

   jogador, escolhedor: caractere
   jogadorVerificado: caractere

   casa, posicao, indice: inteiro
   inicioTabuleiro: inteiro

   i, jogosAbertos: inteiro

   terminouCasa, venceuCasa: logico
   casaValida, jogadaValida: logico
   reiniciou: logico

   fimJogo, venceuX, venceuO: logico


// Verifica se ainda existe possibilidade de vitoria
funcao possibilidade(): logico
inicio

   // Primeira linha
   se ((tabuleiro[inicioTabuleiro+1] = " ") ou (tabuleiro[inicioTabuleiro+1] = jogadorVerificado)) e ((tabuleiro[inicioTabuleiro+2] = " ") ou (tabuleiro[inicioTabuleiro+2] = jogadorVerificado)) e ((tabuleiro[inicioTabuleiro+3] = " ") ou (tabuleiro[inicioTabuleiro+3] = jogadorVerificado)) entao
      retorne verdadeiro
   fimse

   // Segunda linha
   se ((tabuleiro[inicioTabuleiro+4] = " ") ou (tabuleiro[inicioTabuleiro+4] = jogadorVerificado)) e ((tabuleiro[inicioTabuleiro+5] = " ") ou (tabuleiro[inicioTabuleiro+5] = jogadorVerificado)) e ((tabuleiro[inicioTabuleiro+6] = " ") ou (tabuleiro[inicioTabuleiro+6] = jogadorVerificado)) entao
      retorne verdadeiro
   fimse

   // Terceira linha
   se ((tabuleiro[inicioTabuleiro+7] = " ") ou (tabuleiro[inicioTabuleiro+7] = jogadorVerificado)) e ((tabuleiro[inicioTabuleiro+8] = " ") ou (tabuleiro[inicioTabuleiro+8] = jogadorVerificado)) e ((tabuleiro[inicioTabuleiro+9] = " ") ou (tabuleiro[inicioTabuleiro+9] = jogadorVerificado)) entao
      retorne verdadeiro
   fimse

   // Primeira coluna
   se ((tabuleiro[inicioTabuleiro+1] = " ") ou (tabuleiro[inicioTabuleiro+1] = jogadorVerificado)) e ((tabuleiro[inicioTabuleiro+4] = " ") ou (tabuleiro[inicioTabuleiro+4] = jogadorVerificado)) e ((tabuleiro[inicioTabuleiro+7] = " ") ou (tabuleiro[inicioTabuleiro+7] = jogadorVerificado)) entao
      retorne verdadeiro
   fimse

   // Segunda coluna
   se ((tabuleiro[inicioTabuleiro+2] = " ") ou (tabuleiro[inicioTabuleiro+2] = jogadorVerificado)) e ((tabuleiro[inicioTabuleiro+5] = " ") ou (tabuleiro[inicioTabuleiro+5] = jogadorVerificado)) e ((tabuleiro[inicioTabuleiro+8] = " ") ou (tabuleiro[inicioTabuleiro+8] = jogadorVerificado)) entao
      retorne verdadeiro
   fimse

   // Terceira coluna
   se ((tabuleiro[inicioTabuleiro+3] = " ") ou (tabuleiro[inicioTabuleiro+3] = jogadorVerificado)) e ((tabuleiro[inicioTabuleiro+6] = " ") ou (tabuleiro[inicioTabuleiro+6] = jogadorVerificado)) e ((tabuleiro[inicioTabuleiro+9] = " ") ou (tabuleiro[inicioTabuleiro+9] = jogadorVerificado)) entao
      retorne verdadeiro
   fimse

   // Primeira diagonal
   se ((tabuleiro[inicioTabuleiro+1] = " ") ou (tabuleiro[inicioTabuleiro+1] = jogadorVerificado)) e ((tabuleiro[inicioTabuleiro+5] = " ") ou (tabuleiro[inicioTabuleiro+5] = jogadorVerificado)) e ((tabuleiro[inicioTabuleiro+9] = " ") ou (tabuleiro[inicioTabuleiro+9] = jogadorVerificado)) entao
      retorne verdadeiro
   fimse

   // Segunda diagonal
   se ((tabuleiro[inicioTabuleiro+3] = " ") ou (tabuleiro[inicioTabuleiro+3] = jogadorVerificado)) e ((tabuleiro[inicioTabuleiro+5] = " ") ou (tabuleiro[inicioTabuleiro+5] = jogadorVerificado)) e ((tabuleiro[inicioTabuleiro+7] = " ") ou (tabuleiro[inicioTabuleiro+7] = jogadorVerificado)) entao
      retorne verdadeiro
   fimse

   retorne falso

fimfuncao


// Verifica se o jogador venceu
funcao ganhou(): logico
inicio

   // Linhas
   se (tabuleiro[inicioTabuleiro+1] = jogadorVerificado) e (tabuleiro[inicioTabuleiro+2] = jogadorVerificado) e (tabuleiro[inicioTabuleiro+3] = jogadorVerificado) entao
      retorne verdadeiro
   fimse

   se (tabuleiro[inicioTabuleiro+4] = jogadorVerificado) e (tabuleiro[inicioTabuleiro+5] = jogadorVerificado) e (tabuleiro[inicioTabuleiro+6] = jogadorVerificado) entao
      retorne verdadeiro
   fimse

   se (tabuleiro[inicioTabuleiro+7] = jogadorVerificado) e (tabuleiro[inicioTabuleiro+8] = jogadorVerificado) e (tabuleiro[inicioTabuleiro+9] = jogadorVerificado) entao
      retorne verdadeiro
   fimse

   // Colunas
   se (tabuleiro[inicioTabuleiro+1] = jogadorVerificado) e (tabuleiro[inicioTabuleiro+4] = jogadorVerificado) e (tabuleiro[inicioTabuleiro+7] = jogadorVerificado) entao
      retorne verdadeiro
   fimse

   se (tabuleiro[inicioTabuleiro+2] = jogadorVerificado) e (tabuleiro[inicioTabuleiro+5] = jogadorVerificado) e (tabuleiro[inicioTabuleiro+8] = jogadorVerificado) entao
      retorne verdadeiro
   fimse

   se (tabuleiro[inicioTabuleiro+3] = jogadorVerificado) e (tabuleiro[inicioTabuleiro+6] = jogadorVerificado) e (tabuleiro[inicioTabuleiro+9] = jogadorVerificado) entao
      retorne verdadeiro
   fimse

   // Diagonais
   se (tabuleiro[inicioTabuleiro+1] = jogadorVerificado) e (tabuleiro[inicioTabuleiro+5] = jogadorVerificado) e (tabuleiro[inicioTabuleiro+9] = jogadorVerificado) entao
      retorne verdadeiro
   fimse

   se (tabuleiro[inicioTabuleiro+3] = jogadorVerificado) e (tabuleiro[inicioTabuleiro+5] = jogadorVerificado) e (tabuleiro[inicioTabuleiro+7] = jogadorVerificado) entao
      retorne verdadeiro
   fimse

   retorne falso

fimfuncao


// Verifica se deu velha
funcao empatou(): logico
inicio

   // Verifica se X ainda pode vencer
   jogadorVerificado <- "X"

   se possibilidade() = verdadeiro entao
      retorne falso
   fimse

   // Verifica se O ainda pode vencer
   jogadorVerificado <- "O"

   se possibilidade() = verdadeiro entao
      retorne falso
   fimse

   // Nenhum dos dois possui possibilidade de vitoria
   retorne verdadeiro

fimfuncao


inicio

   // Inicializa todas as 90 posicoes
   para i de 1 ate 90 faca
      tabuleiro[i] <- " "
   fimpara

   // Inicializa as 9 casas
   para i de 1 ate 9 faca
      fechado[i] <- falso
   fimpara

   jogador <- "X"
   escolhedor <- "X"
   jogosAbertos <- 9
   fimJogo <- falso

   venceuX <- falso
   venceuO <- falso


   // JOGO PRINCIPAL
   enquanto fimJogo = falso faca

      escreval("")
      escreval("TABULEIRO PRINCIPAL")
      escreval("|", tabuleiro[82], "|", tabuleiro[83], "|", tabuleiro[84], "|")
      escreval("|", tabuleiro[85], "|", tabuleiro[86], "|", tabuleiro[87], "|")
      escreval("|", tabuleiro[88], "|", tabuleiro[89], "|", tabuleiro[90], "|")

      reiniciou <- falso

      // ESCOLHA DA CASA
      casaValida <- falso

      repita

         escreval("")
         escreval("Jogador ", escolhedor, ", escolha uma casa de 1 a 9:")
         leia(casa)

         se (casa >= 1) e (casa <= 9) entao

            se fechado[casa] = falso entao
               casaValida <- verdadeiro
            senao
               escreval("Essa casa ja foi fechada. Escolha outra.")
            fimse

         senao
            escreval("Escolha um numero entre 1 e 9.")
         fimse

      ate casaValida


      // CALCULA O INDICE DA CASA
      indice <- (casa - 1) * 9

      // Quem escolheu a casa comeca jogando
      jogador <- escolhedor

      terminouCasa <- falso
      venceuCasa <- falso


      // JOGO MENOR
      enquanto terminouCasa = falso faca

         escreval("")
         escreval("Casa ", casa, ":")
         escreval("|", tabuleiro[indice+1], "|", tabuleiro[indice+2], "|", tabuleiro[indice+3], "|")
         escreval("|", tabuleiro[indice+4], "|", tabuleiro[indice+5], "|", tabuleiro[indice+6], "|")
         escreval("|", tabuleiro[indice+7], "|", tabuleiro[indice+8], "|", tabuleiro[indice+9], "|")

         // ESCOLHA DA POSICAO
         jogadaValida <- falso

         repita

            escreval("Jogador ", jogador, ", escolha uma posicao de 1 a 9:")
            leia(posicao)

            se (posicao >= 1) e (posicao <= 9) entao

               se tabuleiro[indice + posicao] = " " entao
                  jogadaValida <- verdadeiro
               senao
                  escreval("Essa posicao ja esta ocupada.")
               fimse

            senao
               escreval("Escolha um numero entre 1 e 9.")
            fimse

         ate jogadaValida


         // REGISTRA A JOGADA
         tabuleiro[indice + posicao] <- jogador

         // Define qual tabuleiro sera verificado
         inicioTabuleiro <- indice
         jogadorVerificado <- jogador


         // VERIFICA PRIMEIRO SE HOUVE VITORIA
         se ganhou() = verdadeiro entao

            escreval("Jogador ", jogador, " venceu essa casa!")

            // Marca a casa no tabuleiro principal
            tabuleiro[81 + casa] <- jogador

            terminouCasa <- verdadeiro
            venceuCasa <- verdadeiro

         senao

            // VERIFICA VELHA IMEDIATAMENTE APOS A JOGADA
            se empatou() = verdadeiro entao

               escreval("Deu velha! A casa continuara disponivel.")

               // Apaga somente as 9 posicoes dessa casa
               para i de 1 ate 9 faca
                  tabuleiro[indice + i] <- " "
               fimpara

               // A casa permanece aberta
               terminouCasa <- verdadeiro

            senao

               // ALTERNA O JOGADOR
               se jogador = "X" entao
                  jogador <- "O"
               senao
                  jogador <- "X"
               fimse

            fimse

         fimse

      fimenquanto


      // FECHA A CASA SOMENTE SE ALGUEM VENCEU
      se venceuCasa = verdadeiro entao

         fechado[casa] <- verdadeiro
         jogosAbertos <- jogosAbertos - 1

      fimse


      // VERIFICA O TABULEIRO PRINCIPAL
      se venceuCasa = verdadeiro entao

         inicioTabuleiro <- 81

         // Verifica vitoria de X
         jogadorVerificado <- "X"
         venceuX <- ganhou()

         // Verifica vitoria de O
         jogadorVerificado <- "O"
         venceuO <- ganhou()


         // Se alguem venceu, encerra o jogo
         se venceuX ou venceuO entao

            fimJogo <- verdadeiro

         senao

            // VERIFICA SE O JOGO PRINCIPAL DEU VELHA
            se empatou() = verdadeiro entao

               escreval("")
               escreval("Deu velha no jogo grande! Reiniciando o jogo inteiro.")

               // Apaga todas as 90 posicoes
               para i de 1 ate 90 faca
                  tabuleiro[i] <- " "
               fimpara

               // Reabre todas as casas
               para i de 1 ate 9 faca
                  fechado[i] <- falso
               fimpara

               jogosAbertos <- 9

               // Reinicia os jogadores
               jogador <- "X"
               escolhedor <- "X"

               venceuX <- falso
               venceuO <- falso

               reiniciou <- verdadeiro

            fimse

         fimse

      fimse


      // ALTERNA QUEM ESCOLHE A PROXIMA CASA
      // Nao alterna se o jogo inteiro foi reiniciado
      // Tambem nao alterna se alguem venceu o jogo principal
      se (reiniciou = falso) e (fimJogo = falso) entao

         se escolhedor = "X" entao
            escolhedor <- "O"
         senao
            escolhedor <- "X"
         fimse

      fimse

   fimenquanto


   // MOSTRA O TABULEIRO FINAL
   escreval("")
   escreval("TABULEIRO PRINCIPAL FINAL")
   escreval("|", tabuleiro[82], "|", tabuleiro[83], "|", tabuleiro[84], "|")
   escreval("|", tabuleiro[85], "|", tabuleiro[86], "|", tabuleiro[87], "|")
   escreval("|", tabuleiro[88], "|", tabuleiro[89], "|", tabuleiro[90], "|")


   // ANUNCIA O VENCEDOR
   se venceuX = verdadeiro entao

      escreval("")
      escreval("Jogador X venceu o jogo!")

   senao

      se venceuO = verdadeiro entao
         escreval("")
         escreval("Jogador O venceu o jogo!")
      fimse

   fimse

fimalgoritmo
