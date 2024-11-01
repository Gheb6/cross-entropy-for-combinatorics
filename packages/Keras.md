**Keras** è una libreria open source per il deep learning e le reti neurali, scritta in Python. 
È progettata per essere facile da usare e modulare, permettendo di costruire e addestrare modelli di deep learning in modo rapido e intuitivo.

Ecco un breve riassunto delle sue caratteristiche principali:
1. API di alto livello: Keras fornisce un’interfaccia semplice e intuitiva per definire e addestrare modelli di deep learning.
2. Compatibilità con backend: Supporta diversi motori di calcolo come TensorFlow, Theano e Microsoft Cognitive Toolkit (CNTK), che eseguono i calcoli di basso livello.
3. Modularità: È altamente modulare, permettendo di combinare diversi moduli (livelli, funzioni di attivazione, ottimizzatori, ecc.) per creare modelli complessi.

Keras è ampiamente utilizzata sia nella ricerca che nell’industria per sviluppare applicazioni di intelligenza artificiale, grazie alla sua semplicità e flessibilità.

from keras.models import Sequential
    Importare il modello Sequential dalla libreria Keras. Sequential è un tipo di modello che permette di costruire una rete neurale strato per strato.

model = Sequential()
    Creare un’istanza del modello Sequential

model.add(Dense(FIRST_LAYER_NEURONS, activation="relu"))
model.add(Dense(SECOND_LAYER_NEURONS, activation="relu"))
model.add(Dense(THIRD_LAYER_NEURONS, activation="relu"))

Dense è un tipo di livello completamente connesso. Ogni neurone di un livello è connesso a tutti i neuroni del livello precedente.
FIRST_LAYER_NEURONS, SECOND_LAYER_NEURONS, e THIRD_LAYER_NEURONS sono variabili 
che rappresentano il numero di neuroni nei rispettivi livelli.

activation="relu" specifica la funzione di attivazione ReLU (Rectified Linear Unit) per i primi tre livelli. 
ReLU è una funzione di attivazione molto comune nelle reti neurali.

model.add(Dense(1, activation="sigmoid"))
    L’ultimo livello ha un solo neurone (Dense(1)) con una funzione di attivazione sigmoid, spesso usata per problemi di classificazione binaria.

model.build((None, observation_space))
    Definizione forma dell'input del modello. 
    observation_space rappresenta il numero di caratteristiche dell’input. None indica che il modello può accettare un numero variabile di campioni.

model.compile(loss="binary_crossentropy", optimizer=SGD(learning_rate = LEARNING_RATE))
    loss="binary_crossentropy" specifica la funzione di perdita da usare, adatta per problemi di classificazione binaria.
    optimizer=SGD(learning_rate = LEARNING_RATE) indica l’uso dell’ottimizzatore Stochastic Gradient Descent (SGD)
    con un tasso di apprendimento specificato da LEARNING_RATE.
