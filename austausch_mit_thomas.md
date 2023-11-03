


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