```mermaid
flowchart TD
  Start([Inicio])
  Init[/"Inicializar parámetros:\nS=7, R=9, ep=0.1"/]
  CreateW1["Definir W1 (matriz 7x9)\nDefinir v_p (vector entrada)"]
  Bias["Calcular bias:\nb = R\nb1 = b * ones(S,1)"]
  FeedForward["ETAPA FEEDFORWARD:\nn1 = W1 * v_p + b1\na1 = n1"]
  CreateW2["Crear W2 (recurrente):\nW2 = I - ep*(ones- I)"]
  InitRec["Inicializar\nepocas=100\nresp_prev=zeros(S,1)\nhistorico=zeros(S,epocas)\ni=1"]
  LoopStart{{"i <= epocas?"}}
  CalcN2["n2 = W2 * a1"]
  Poslin["Aplicar poslin:\na2 = max(0,n2)"]
  SaveHist["historico(:,i) = a2"]
  CheckConv{{"¿a2 == resp_prev?"}}
  Converge["Imprimir convergencia\ny recortar 'historico'"]
  UpdatePrev["resp_prev = a2"]
  UpdateA1["a1 = a2\ni = i + 1"]
  EndLoop(("Fin Bucle"))
  Winner["Determinar ganador:\n[~, ganador] = max(a2)\nImprimir clase ganadora"]
  Plot["Graficar 'historico'"]
  End([Fin])

  Start --> Init --> CreateW1 --> Bias --> FeedForward --> CreateW2 --> InitRec --> LoopStart
  LoopStart -- Sí --> CalcN2 --> Poslin --> SaveHist --> CheckConv
  CheckConv -- Sí --> Converge --> EndLoop
  CheckConv -- No --> UpdatePrev --> UpdateA1 --> LoopStart
  LoopStart -- No --> EndLoop
  EndLoop --> Winner --> Plot --> End
