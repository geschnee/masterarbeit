# MIttwoch 29.12.


# Vortrag 

(siehe Presentation PDF von Maximilian)

* previous work (nicht unbedingt alle 3 Arbeiten)
* Forschungsfragen
* Reinforcemente Learning + Durchfuehrung (unterschiede zur Arbeit von Max) (end to end + reward shaping...)
* Stand der Forschung zeigen
    * besonders da noch keine Ergebnisse vorhanden sind
    * sehr wichtig Thomas!!!
    * drei Ergebnisse aus vorherigen papers zeigen
* Exeperimente ich dann am Ende durchfuehren moechte


# Expose

## erledigt
numerierung der 4 Forschungsfragen

pruefen, ob die Research Goals wirklich messbar sind
(ist diese Frage beantwortet?)

subfrage 1 zum Memory kann ich entfernen und das frame stacking nicht als extra Frage behandeln


Expose muss klar die Abtrennung zu Max zeigen:
* CNN statt pipeline
* bessere Reward shaping
* Trainign mit Ziel Robustheit gegenueber Aenderungen der Umgebung
    * unterschiedliche Lichtverhaeltnisse im Training
    * data augmentation ...

Expose muss die Robustheit gegenueber Lightaenderungen klar definieren

alle Fragen aus Research Goals numerieren und konkret die Vorgehensweise zur Beantwortung aufschreiben im Expose

zur JetBot subfrage:
Is it possible to use a CNN which is small enough to be used in the JetBot?
    * Beantworten der Frage muss erklaert werden
    * mit Unterstuetung des Teams werden wir das Model auf dem JetBot testen
    * testen mit reduziertem CNN model
    * Replay in Python + Unity erstellen
        * das CNN auf den JetBot uebertragen
        * Replay auf dem JetBot abspielen
        * schafft der JetBot es die Outputs aus dem Replay in der Zeit zu reproduzieren?



aus email:

ich habe Dein Expose bis einschließlich Kap. 3 gelesen.

Verbesserungsvorschläge:

+ Aussagen mit Quellen belegen (z.B. S. : ..."traffic accidents und
transportation const")

+ Abstract: self driving cars, noch zu wenig präzise und "the work will
compared to the results of the previous thesis" (das ist vielleicht
qualitativ möglich, aber nicht quantitativ);  "The goals ist to improve
the agent's performance..." (zu wenig messbar...)

+ Abschnitt Research Goal: "...is trained and evaluated on a simulated
parcour"  ...der Parkour wird nicht simuliert....warum schreibst Du
englischsprachig, bist Du Dir sicher Dich in der englischen Sprache
ausreichend präzise ausdrücken zu können und dabei noch Rechtschreibung
und Grammatik richtig anzuwenden?

+ Abschnitt Reseach Goal: noch zu unpräzise, wie gestern besprochen

+ Abschnitt Related Work: umfangreich, für ein Expose eigentlich zu
umfangreich, aber gleichzeitig zu oberflächlich und gleichzeitig nicht
ausreichend verständlich beschrieben was jeweils erreicht wurde und
welchen Nutzen Du für Deine Arbeit daraus ziehst und wo Du dich
abgrenzen möchtest. Also musst Du spätestens in dre Arbeit Substanz
liefern und am Ende auch Stärken und Schwächen der Beiträge (related
Work) diskutieren.


Fazit: Du bist auf dem richtigen Weg, aber es fällt Dir noch schwer Dich
präzise und kurz zu fassen. Es ist eine gute Übung, Dein Expose auf die
Hälfte zu kürzen und dabei nicht an Informationsgehalt zu verlieren. Im
Expose musst du auch noch nicht alles bildlich darstellen.

In Deinen  Vortragsfolien in 2 Wochen sind die Bilder wichtig und tragen
zur Anschaulichkeit bei.




## Papa

- Spuren tracking zur Visualisierung (alle Spuren uebereinandergelegt gibt gutes Bild fuer evaluation)
- anzeige einer guten Spur um zu zeigen, dass es ein Parcour/Rennstrecke ist / Visualisierung der Dynamik
- andere preprocessing schritte testen, als alternative zu histogram equalization
- histogram equalization bilder mit verschiedenen Lichtparameter in der Arena zeigen
- mit den verschiedenen Lichtparametern und bildern, konnte man sehen welche Preprocessing Schritte gut sind

bezug zum Scads.AI herstellen um Arenadesign zu begrunden
Bezug zu Max fuer Motivation zum Roboterdesign und Parcours



# JetBot

es sieht so aus, als könnte der JetBot resnet-18 verarbeiten (18 Layer Neuronales Netzwerk)
https://github.com/NVIDIA-AI-IOT/jetracer/blob/master/notebooks/interactive_regression.ipynb

JetBot nimmt Jupyter notebooks:
https://jetbot.org/master/

man könnte ein Replay Notebook schreiben


# 07.12.

vor den Research questions muss klar sein, was der Input und der Output ist und dass der Agent mit Reinforcement Learning trainienrt wird
(passt gut zur Folie autonomous drivign task)


Previous Work Sektion

uebersicht ueber die RL algorithmen zeigen, Auswahl des PPOs begruenden

nicht auf Max warten mit den Lichtverhaeltnissen, alles was er nicht angegeben hat kann ich selbst machen wie ich will

Folie zu Data Augmentation?