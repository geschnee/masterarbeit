


# Light Invariant Video Imaging for Improved Performance of Convolution Neural Networks

- das Paper stellt LIVI imaging vor, was eine extra Lichtquelle benötigt um Bilder licht-invariant zu machen
- zusätzlich verwenden sie Image augmentation um mehr Trainingsdaten zu erhalten
- die Analysieren die Neuronalen Netzwerk Aktivierungen in verschiedenen Lichtverhältnissen
    - sie kommen zu dem Schluss dass Farbinformationen sehr wichtig sind (bessere Performance als grayscale)


mögliche Ansätze um ein Bild light invariant zu machen (ohne extra lichtquelle im Bild):
- WB using gray edge ?



# white balancing grey world

https://de.mathworks.com/help/images/comparison-of-auto-white-balance-algorithms.html

sieht echt gut aus!!!
https://www.youtube.com/watch?v=RXvx2pNDR9E


# Perception and sensing for autonomous vehicles under adverse weather conditions: A survey

- überblick über Sensoren in Autonomen Fahrzeugen und wie Wetter diese Sensoren beeinflussen
- Car Cameras use fisheye lenses for wide field of view
- Beschreibung des Einflusses von hoher Lichtintensität auf Cameras

Lösungen
- Multimodal sensors (Fusion) zum Verringern der neg. Einflüsse
- Cameras like long-wave infrared are often used
- using a neural network for de-raining (removing the impact of rain from an image)
    - often used a NN to generate the images first / encoder-decoder
- image dehazing approaches based on image processing
    - Histogram Equalization Kim et al., 1998, 
    - Negative Correlation Gao et al., 2014, 
    - Homomorphic Filter Shen et al., 2014,
    - Retinex Zhou and Zhou, 2013, etc.

- Sektion 4.4. für Licht Intensität

