


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

- Zeit zwischen Schritten ist sehr gross, vielleicht deswegen nicht gut lernfaehig


# 16.01.2024

- zwischenstufe aus Fixed und Random Spawn
- Agent mit geringer zufaelliger Rotation an festem Platz mit Orientierungsreward um zu lernen auf das erste Tor zu fahren

- Training auf einfachem Scenario mit fixiertem Spawnpoint und aber (weniger) zufaelliger Rotation
    - Agent soll erstmal lernen durch das erste Tor zu fahren
    - Orientation Reward

- Zeit zwischen Schritten untersuchen, warum sind die Zeiten sehr lang?
    - time/fps Metrik?
    - mean_episode_length
    - geringe mean_episode_length --> Agent kann nicht reagieren/lernen
    - weniger Environments


- keine Beendung der Episode bei Kollisionen
- Abbruch nur bei Timeout und wenn das Ziel erreicht wurde
    - Agent kann theoretisch von der Map fallen (Waende muessen hoeher sein)

- Unterschied zwischen Roboter in Simulation und Realitaet
    - Roboter Kamera Sichtfeld
    - Roboter Lenkwinkel statt Geschwindigkeitsunterschiede
    - Roboter Variante mit festen Raedern + Kugel erstellen



