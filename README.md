# Transcritor de Aula (versão 2)

Cópia evoluída do `plaud-note-online-transcricao-de-audio` (a original não foi alterada). Página estática (sem servidor): abre direto no navegador ou no GitHub Pages.

## O que a versão 2 acrescenta: Modo aula (padrão)
- Grava em blocos (1, 2, 5 ou 10 min), corta numa pausa na fala, abre o próximo bloco sem lacuna e transcreve o anterior.
- Só o texto fica guardado: o áudio do bloco (Opus, ~3 KB/s) é apagado depois que o texto é salvo. O áudio pendente fica no IndexedDB; se a página cair, o botão "Processar blocos pendentes" retoma.
- Whisper no próprio celular (transformers.js em Worker; WebGPU se houver, senão WASM): modelos tiny, base (padrão) e small.
- Alternativa: Gemini (chave do Google AI Studio guardada só no aparelho; áudio vai para o Google). A página troca sozinha do Whisper para o Gemini, ou para um modelo mais leve, se a transcrição ficar mais lenta que a gravação.
- ETL automático ao parar (mesmo da versão 1). Os modos ao vivo da versão 1 (Chrome e Whisper) continuam disponíveis.

## Testado
- Ciclo completo no Chrome do computador com microfone simulado: 3 blocos, cortes nas pausas, texto completo, áudio apagado, ETL automático.
- Recuperação de bloco pendente após recarregar a página.
- Gemini só com resposta simulada (sem chave real).
- NÃO testado: Android real (velocidade do Whisper, tela apagada, bateria), WebGPU, internet móvel.

## Armazenamento próprio
Usa chaves `transcritor_aula_*` e o banco `transcritor_aula`, separados da versão 1.
