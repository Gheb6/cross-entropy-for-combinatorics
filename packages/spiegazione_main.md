## 1. Creazione delle sessioni
- for i in range(1000000)\
Il ciclo principale esegue 1.000.000 iterazioni (o generazioni) per il processo di addestramento.

- tic = time.time()
- sessions = generate_session(model, n_sessions, 0)\
  generate_session: Genera un insieme di "sessioni" (ossia episodi di addestramento) con il modello corrente. Ogni sessione contiene stati, azioni e premi.
- sessgen_time = time.time() - tic\
sessgen_time: Misura il tempo necessario per generare queste sessioni.

## 2. Preparazione delle sessioni e dei batch

- states_batch = np.array(sessions[0], dtype=int)
- actions_batch = np.array(sessions[1], dtype=int)
- rewards_batch = np.array(sessions[2])
- states_batch = np.transpose(states_batch, axes=[0,2,1])\
np.transpose(states_batch, axes=[0,2,1]): Cambia l'ordine degli assi per adattarlo al formato richiesto dal modello.
- states_batch = np.append(states_batch, super_states, axis=0)
- if i > 0:
    - actions_batch = np.append(actions_batch, np.array(super_actions), axis=0)
- rewards_batch = np.append(rewards_batch, super_rewards)\
Aggiunge le sessioni "super" (vedi sotto) ai batch di addestramento.
Le variabili super_states, super_actions, e super_rewards contengono le migliori sessioni delle iterazioni precedenti.

## 3. Selezione degli "elite" e "super" sessioni

- elite_states, elite_actions = select_elites(states_batch, actions_batch, rewards_batch, percentile=percentile)\
select_elites: Seleziona i migliori stati e azioni (dati un certo percentile) per l’addestramento.

- super_sessions = select_super_sessions(states_batch, actions_batch, rewards_batch, percentile=super_percentile)
- super_sessions = [(super_sessions[0][i], super_sessions[1][i], super_sessions[2][i]) for i in range(len(super_sessions[2]))]
- super_sessions.sort(key=lambda super_sessions: super_sessions[2], reverse=True)\
select_super_sessions: Seleziona le migliori sessioni complete per essere salvate.
Le sessioni selezionate vengono ordinate in ordine decrescente di premio, per mantenere solo le migliori.

## 4. Addestramento del modello
- model.fit(elite_states, elite_actions)\
Addestra il modello utilizzando solo le sessioni "elite"

## 5. Aggiornamento delle sessioni "super"

- super_states = [super_sessions[i][0] for i in range(len(super_sessions))]
- super_actions = [super_sessions[i][1] for i in range(len(super_sessions))]
- super_rewards = [super_sessions[i][2] for i in range(len(super_sessions))] \
Aggiorna super_states, super_actions, e super_rewards per la prossima iterazione.

## 6. Calcolo delle metriche
- rewards_batch.sort()
- mean_all_reward = np.mean(rewards_batch[-100:])
- mean_best_reward = np.mean(super_rewards) \
mean_all_reward: Media degli ultimi 100 premi del batch, rappresenta una media su tutti gli episodi.
mean_best_reward: Media dei premi delle migliori sessioni selezionate.


