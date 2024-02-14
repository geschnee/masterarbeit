


# 17.10.2023
* Erstmal nicht auf sim2reality Gap gehen
* Max hätte etwas zu wenig in die existierende Forschung geguckt
* gut wäre es in Simulation zu trainieren mit eigenen Verbesserungen und die Experimente von Max zu schlagen

# 24.10.2023

Hallo Georg,

mein Entwurf für die Forschungsfragen:

Frage 1. Mit welcher Erfolgsquote kann das Fahrzeug in der Simulation den
vollständigen Parkour bewältigen (Kollisionen sind als Negativereignisse
in der Reward-Funktion zu berücksichtigen). Die Metrik Erfolgsquote
berechnet das Verhältnis erfoglreich absolvierter Parkour-Fahrten zu
allen Parkour-Fahrten. Eine Begrennzung auf maximal 3 Mio
Trainingsschritte ist zu berücksichtigen (ist die Orientierung an dem
Wert aus der Arbeit von Max sinnvoll?)

Unterfrage: Eine Gedächtnisfunktion ist vorzuschlagen, zu implementieren und
zu evaluieren und dem Betrieb ohne Gedächtnisfunktion
gegenüberzustellen. Kann das LSTM in dem Anwendungsbereich einen Nutzen
bringen? Wenn ja/nein warum?


Frage 2. Kann das Fahrzeug in der Simulation bei unterschiedlichen
Lichtverhältnissen den Parkour erfolgreich bewältigen (Metrik
Erfolgsqoute), wenn für die Verarbeitung der Bilddaten ein CNN verwendet
wird.

Unterfrage: Es ist ein CNN auszuwählen, welches auf einem NVIDIA Jetson Nano
mit einer Bildsequenz von 30 Bilder je Sekunde die erforderlichen
Ausgangssignale verzögerungsfrei erzeugen kann.

Terminvorschlag: 8.11 um 15 Uhr.

Grüße Thomas

# 08.11.2023

- Experimente zur varying Motorpower können weggelassen werden
- Expose sollte vor dem Vortrag am 15.12. fertig sein
- Arbeit sollte auch angemeldet sein
- wie? ein Dokument vom Prüfungsamt ausdrucken, ausfüllen und an Thomas geben

TODO 
- Field of view für den Roboter prüfen
- Framerate prüfen

# 03.01.2024

- 1. Gespräch mit Martin Lorenz
- Termin Mittwoch alle 2 Wochen bit Thomas und Martin
- Thomas wird am Ende eine Note geben und Martin eine Bewertungsempfehlung an Rahm und dieser gibt dann eine Note
    - Ergebnis beider Noten ist dann das Endergebnis
- keine weiteren Gespräche mit Professor Rahm zusammen zu erwarten
- Martin hat sich mit RL in einer Grid-Umgebung beschäftigt (sb3)
- als nächstes Experimentierung mit Reward Function

Ziele bis nächstes Meeting:
- EventReward warum reward 100 für das letzte Tor?, warum nicht 1?
- kann der Agent mit Random Spawn und fixed spawn zuverlässig das erste Tor erreichen?
    - vielleicht weitwinkel Kamera input verwenden
- profiling um Training schneller zu machen

Ergbenisse Zwischenzeit:
- fixed spawn hat bis jetzt nur geradeausfahren gelernt
- random spawn ist nicht gut durch die Tore gefahren
- Maximilian hat random im Training und Fixed in der Bewertung genommen

- mehr Logging Metriken in Tensorboard
- Ausgliederung in Config Datei

- Zeit zwischen Schritten ist sehr gross, vielleicht deswegen nicht gut lernfähig


# 16.01.2024

## learn something
- zwischenstufe aus Fixed und Random Spawn
- Agent mit geringer zufälliger Rotation an festem Platz mit Orientierungsreward um zu lernen auf das erste Tor zu fahren

- Training auf einfachem Scenario mit fixiertem Spawnpoint und aber (weniger) zufälliger Rotation
    - Agent soll erstmal lernen durch das erste Tor zu fahren
    - Orientation Reward

### Ergebnisse

- neuer Parameter in Config: env_kwargs.spawn_point
    - Fixed, OrientationRandom, OrientationVeryRandom and FullyRandom
- eval_medium/success_rate von 95% mit spawn OrientationVeryRandom:
{'comment': 'now trying again with fixed spawn pos but fully 45 Degree random spawn orientation, can it still reach success rate of 1 for easy parcour?', 'n_envs': 10, 'num_evals_per_difficulty': 20, 'n_epochs': 5, 'log_interval': 5, 'batch_size': 64, 'n_steps': 64, 'copy_model_from': False, 'env_kwargs': {'jetbot': 'DifferentialJetBot', 'spawn_point': 'OrientationVeryRandom', 'single_goal': False, 'frame_stacking': 3, 'image_preprocessing': {'grayscale': True, 'equalize': True, 'contrast_increase': 'TODO', 'normalize_images': False}, 'coefficients': {'distanceCoefficient': 0.5, 'orientationCoefficient': 0.0, 'velocityCoefficient': 0.0, 'eventCoefficient': 1.0}, 'trainingMapType': 'randomEvalEasy', 'width': 500, 'height': 168}}
- print_states_after_reset.py shows that for OrientationVeryRandom the first goal in some medium and hard parcours is not fully in the camera field after reset
- print_states_after_reset.py shows that for OrientationRandom the first goal in some hard parcours is not fully in the camera field after reset

## Step time
- Zeit zwischen Schritten untersuchen, warum sind die Zeiten sehr lang?
    - time/fps Metrik?
    - mean_episode_length
    - geringe mean_episode_length --> Agent kann nicht reagieren/lernen
    - weniger Environments

### Ergebnisse

- kein Performance Unterschied zwischen Editor und Windows standalone festgestellt (auf Laptop)
- Editor ist schneller als Windows standalone auf dem Home PC (percall time 0.02 in Editor versus 0.05 in Windows standalone für unity_comms.py:129(rpc_call))
- Home PC schneller als Laptop

- Problem war der Parallelitätsgrad
    - Laptop in Editor mit n_env 50 percall time 0.08 vs n_env 10 percall time 0.04


- Constante Timesteplaenge wurde implementiert, es muss aber noch getestet/trainiert werden
    - definiert in cfg.env_kwargs.fixedTimestepsLength
    - keine Physik in der Arena nach Ablauf der Zeit bis naechste Aktion zugewiesen ist

## Endevents
- keine Beendung der Episode bei Kollisionen
- Abbruch nur bei Timeout und wenn das Ziel erreicht wurde
    - Agent kann theoretisch von der Map fallen

### Ergebnisse
- wurde umgesetzt
- Wände wurden erhöht, damit der Agent nicht von der Arena fallen kann


## Sim Reality Diff
- Unterschied zwischen Roboter in Simulation und Realität
    - Roboter Kamera Sichtfeld
    - Roboter Lenkwinkel statt Geschwindigkeitsunterschiede
    - Roboter Variante mit festen Rädern + Kugel erstellen

### Ergebnisse

- DifferentialJetBot gebaut
    - bessere Performance als der vorherige JetBot
- Reverse Controller in car-following_carla_dresden seht interessant aber definitiv out of scope für diese Arbeit









# 31.01.2024

Hauptpunkt
- Grafik fuer trainingsaufbau/Algorithmus schreiben (collect, train eval Loop)
- Terminologien festlegen in den Grafiken


nächste TODOS:

- Bewertungen mit mehr Episoden testen (nicht nur 20)
- Videos fuer gute durchlaufe aufnehmen
    - https://gist.github.com/DashW/74d726293c0d3aeb53f4
- untersuchen warum die Performance bei spaeteren Iterationen nachlaesst
    - zu wenig data collection
        - fast perfekte Performance für easy und medium Setting, totaler Absturz für hard Setting ab einem gewissen Punkt 08-08-2024/10....
        - {'comment': 'Trying with more n_steps, does the performance still drop off after a while? does it drop off later?', 'n_envs': 10, 'num_evals_per_difficulty': 20, 'n_epochs': 5, 'log_interval': 5, 'batch_size': 64, 'n_steps': 256, 'copy_model_from': False, 'env_kwargs': {'jetbot': 'StandardJetBot', 'spawn_point': 'OrientationRandom', 'frame_stacking': 10, 'image_preprocessing': {'grayscale': True, 'equalize': True, 'contrast_increase': 'TODO', 'normalize_images': False}, 'coefficients': {'distanceCoefficient': 0.5, 'orientationCoefficient': 0.0, 'velocityCoefficient': 0.0, 'eventCoefficient': 1.0}, 'trainingMapType': 'randomEval', 'fixedTimestepsLength': False, 'width': 500, 'height': 168}}
    - Stabilitaet
- DifferentialJetBot mit FixedSpawn und randomEval map testen
- StandardJetBot nochmal testen
    - wenn der nicht so gut ist, dann immer DifferentialJetBot verwenden
    - Run 2024-02-04\11-56-53\tmp\PPO_1 vom Desktop PC zeigt der StandardJetBot kann auch gute Ergebnisse erzielen
    - {'comment': 'Trying with StandardJetBot again, can it reach the performance of the DifferentialJetBot with the same settings?', 'n_envs': 10, 'num_evals_per_difficulty': 20, 'n_epochs': 5, 'log_interval': 5, 'batch_size': 64, 'n_steps': 64, 'copy_model_from': False, 'env_kwargs': {'jetbot': 'StandardJetBot', 'spawn_point': 'OrientationRandom', 'frame_stacking': 10, 'image_preprocessing': {'grayscale': True, 'equalize': True, 'contrast_increase': 'TODO', 'normalize_images': False}, 'coefficients': {'distanceCoefficient': 0.5, 'orientationCoefficient': 0.0, 'velocityCoefficient': 0.0, 'eventCoefficient': 1.0}, 'trainingMapType': 'randomEval', 'fixedTimestepsLength': False, 'width': 500, 'height': 168}}
- fixedLength testen


# 14.02.2024

- Clinicum Digitale 2024 in Dresden
    - Lehrgang für Medizin und Informatik
    - 18.03.2024 bis 27.03.2024 statt.
    - https://digitalhealth.tu-dresden.de/career-education/students/clinicum-digitale/ 
- Wort Game aus Codebase und Algorithmus beschreibung entfernen
    - Sollte stattdessen Episode sein https://en.wikipedia.org/wiki/Proximal_Policy_Optimization
    - nochmal mit Barto Buch gegenprüfen