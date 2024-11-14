## Numpy
NumPy è una libreria open-source che supporta operazioni matematiche e logiche su array di grandi dimensioni e matrici. 
È particolarmente utile per l’elaborazione di dati numerici e per l’implementazione di algoritmi scientifici.
Caratteristiche principali:
Array multidimensionali: NumPy introduce l’oggetto ndarray, che è un array N-dimensionale omogeneo, molto più efficiente rispetto alle liste native di Python.
Funzioni matematiche: Include una vasta gamma di funzioni matematiche per operazioni su array, come algebra lineare, 
trasformate di Fourier, e generazione di numeri casuali.

- np.zeros([n_sessions, observation_space, len_game], dtype=int)
    crea un array multidimensionale di zeri con una forma specificata e un tipo di dato intero. Array risultante avrà 3 dimensioni:
    n_sessions: Il numero di sessioni.
    observation_space: Lo spazio di osservazione per ogni sessione.
    len_game: La lunghezza del gioco o il numero di passi temporali per ogni osservazione.

- La funzione np.random.rand()
    genera un array di numeri casuali con una distribuzione uniforme nell’intervallo [0, 1)

- np.percentile(rewards_batch, percentile) calcola il valore del percentile specificato per un array di dati:
    rewards_batch: Questo è l’array di dati per il quale vuoi calcolare il percentile
    percentile: Questo è il percentile che vuoi calcolare, espresso come un numero tra 0 e 100.
      Ad esempio, se percentile è 50, la funzione calcolerà il valore mediano dell’array
- np.array(elite_states, dtype=int) ##riga 223
    converte l’input elite_states in un array NumPy di tipo intero

- super_states =  np.empty((0,len_game,observation_space), dtype = int)
        crea un array vuoto con una forma specificata e un tipo di dato intero:
            La prima dimensione è 0, il che significa che l’array inizialmente non contiene elementi lungo questa dimensione.
            len_game: La lunghezza del gioco o il numero di passi temporali.
            observation_space: la terza dimensione avrà una lunghezza pari al valore di observation_space

  ## Metodo transpose
  riga 278 states_batch = np.transpose(states_batch,axes=[0,2,1])
  import numpy as np
 Matrice 3D con due strati, 3 righe e 4 colonne
a = np.array([[[1, 2, 3, 4], [5, 6, 7, 8], [9, 10, 11, 12]],
              [[13, 14, 15, 16], [17, 18, 19, 20], [21, 22, 23, 24]]])

print(a)
a=np.transpose(a, axes=[0,2,1])  
print("!")
print(a)

output:
[[[ 1  2  3  4]
  [ 5  6  7  8]
  [ 9 10 11 12]]

 [[13 14 15 16]
  [17 18 19 20]
  [21 22 23 24]]]
!
[[[ 1  5  9]
  [ 2  6 10]
  [ 3  7 11]
  [ 4  8 12]]

 [[13 17 21]
  [14 18 22]
  [15 19 23]
  [16 20 24]]]
