# masterarbeit

## Motivation Idee

Arbeit von Maddi97 war schon sehr erfolgreich in der Simulation
in der Realitaet ist die Preprocessing Pipeline aber abgestuerzt
Ziel:
das Problem loesen in der Realitaet

## Unity as Gym Env
https://github.com/Unity-Technologies/ml-agents

* Train using concurrent Unity environment instances

## Train Unity agent with stable-baselines 3

https://www.youtube.com/watch?v=FqNpVLKSFJg

Communication between Unity and Python
https://github.com/hughperkins/peaceful-pie

## Send data from python to Unity (Socket)
https://www.youtube.com/watch?v=Dm0CiAiZk14

https://www.youtube.com/watch?v=fGHde1h_vaA


## JetBot Roboter

https://developer.nvidia.com/embedded/learn/jetbot


# Notizen zu Maddi97 Masterarbeit
https://github.com/Maddi97/master_thesis

warum sind hier nur 7 Python Skripte? (alle zur Analyse der Ergebnisse)
https://github.com/search?q=repo%3AMaddi97%2Fmaster_thesis%20.py&type=code

generelle Kritik
* so viele Aussagen ohne Begründung
	* Therefore, developing realistic simulated environments offers a safe, cost-effective alternative for training and evaluating algorithms. Furthermore, it is central to divide the problem into small sub-tasks to achieve progress in such a complex challenge.
	* wieso muss man aufteilen??
	* the significant reduction in state size greatly benefits the training process...
		* Er sagt, dass es Experimente ohne Preprocessing gab, beschreibt diese aber nicht weiter. 6.2.1
		* der Memory approach erreicht bessere Ergebnisse als ohne MEM (MAM hat einen größeren Statespace) 
* viel Aussagen wie "Dieses Research paper hilft mir sehr weiter in den Konfigurationen/Research..."
	* wird gesagt wie genau???
* warum wird in Detail erklärt was Unity ist und was és alles kann??? z.B. Unity-Scenes
* warum keine Visualisierung der der Succes-rate während Training?
	* plus Vergleich der final training succes-rate und evaluation succes-rate?
* wie wird der Reward Normalisiert? (Figure 6.3)
	* wenn durch den maximalen CumReward dieses Training Scenarios z.B. PPO-MEM-FMT geteilt wird, ist die unterschiedliche Kurve für die beiden Reward functions SGT und FMT total verständlich
		* der Max reward ist dort größer (weil mehr Zeit in Simulation und mehr Goals)
		* Again drawing the inferences from Figure 6.3, the FMT attempts to convert much slower towards a strong performance. 
		* Der Satz ist Quatsch, da man allein vom Normalized CumReward nicht sagen kann ob die Performance schon gut ist.
		* Besser wäre hier eine Auswertung der Average Completed goals gewesen um die beiden Reward Funktionen vergleichen zu können


wie lang ist jeder Timestep (in Sekunden)? das Environment ist nicht discrete!!!

gibt es Infos zu Tesla's Autopilot (der ist doch mit RL traininert) bzw. ist RL mit Autos in Simulation nicht schon gut untersucht?
* Infos dazu in Section 2.3?


offene Fragen:
* mehrere blaue und rote Blöcke, merkt das Netzwerk wie viele von beiden sind? einmal hab ich wiedersprüchlichen Unity Code gesehen
* Input pro Block: x, y, width und height
	* "precisely the same input as Jonas König"
	* das ist schlecht, weil das NN dann erstmal x + width machen muss um die andere Ecke zu erhalten
	* Bounding Box max_x, min_x, max_y und min_y wäre besser imo
* wieso lenken die Räder in der Simulation, wenn sie in Realität nicht lenken können?
* warum hat der Jetbot in der Simulation 4 Räder und der echte nur 2 Räder + einen Ball (differential steering)?
* enthält die reward function einen reward für Nähe zum nächsten Ziel? oder ähnliches?
	* An example of an issue is that the agent only drives in circles to gain speed reward and, thus, is stuck in a local optima.
	* nein, nur Velocity, Goal, collision and finish episode reward
* zum Experiment mit varying motor powers
	* werden die beide Motoren gleichmäßig angepasst?
	* ja
	* das Experiment sollte die Motoren unterschiedlich anpassen um die Realität besser zu testen


die simulation2reality Gap wirkt für mich interessanter als Ziel der eigenen Arbeit,
da algemeine Fragen wie "Kann RL genutzt werden für autom. driving?" zu schwer zu beantworten sind
Es gibt schon einige Arbeiten mit sim2reality Transfer:
* Self-driving scale car trained by Deep reinforcement learning 
	* self driving roboter mit Training in Simulation und Transfer zu Realität
* Simulated Autonomous Driving Using Reinforcement Learning: A Comparative Study on Unity and ML-Agents Framework


Man kann argumentieren, dass die Unity-Training-Arena von Maximilian ähnlich komplex ist wie ein Atari game

MuZero oder EfficientZero für Automatic driving? (ich meine den Algo der ein World Model selbst erstellt)

Taxonomy of RL
* AlphaGo should be it's own category (search based...)
* AlphaGo zero ist nicht model based meiner Meinung nach	
	* die Erweiterung mit simulierter Transition function hingegen schon




## TODOs:
DQN ist Off-Policy? warum?
PPO ist On-Policy 

Maximilian's Erklärung von Policy-Based Methoden ist gut verständlich
* TODO check: entspricht seine Erklärung der Realität?

### TODOs im Scads.AI

* Arena und Roboter Daten abmessen
* kann der Roboter nur mit differential steering lenken?
	* ja
	* 2 Räder und eine Kugel
* haben die Motoren links und rechts unterschiedliche max Torques?
	* durchaus
* wie sieht ein Bild aus, welches mit der Robo Kamera gemacht wird?
	* Raspberry Camera v2 1080p im Videomodus (1920 x 1080 bei 30fps)


## Notizen aus Discord Call

wie startet man das Training?
* mlagents-learn Befehl startet einen Python Prozess, welcher auf Unity wartet
* man muss eine Unity Scene starten, der Python Prozess uebernimmt dann Kontrolle
* schreibt Ergebnisse zu Tensorboard

Funktioniert Training mit mehreren Envs (parallel) mit dem Setup?
* ja, einfach die ganze Arena duplizieren
* am Ende hat Maximilian das nicht verwendet, da der DataFrame mit den Skripten so nicht funktioniert hat

wie war der Zeitplan?
* arbeiten/vorbereiten bis man bereit ist
* Masterarbeit beantragen
* 6 Monate Zeit
* man kann schon vor Ende der 6 Monate die Arbeit einreichen --> sie wird dann auch frueher bewertet

Wen sollte man nach Hilfe fragen?
* Johannes Häfner (war auch schon im ScadsAI beim ersten Treffen dabei)
* Es gibt noch einen anderen Mitarbeiter im ScadsAI mit Interesse an RL und self-driving

Wie installiert man EmguCV korrekt?
* leider unklar weil lange her
* vielleicht kann jemand mit C# Erfahrung im ScadsAI helfen
* Maximilian hatte das wahrscheinlich selbst kompiliert

Wie war die Benotung / Betreuung?
* Benotung guter Eindruck


Nutzung der echten JetBots?
* die PreprocessingPipeline ist ausserhalb der Simulation zusammengebrochen
* Transfer in die Realitaet ist schwer
    * entweder das ist der Fokus der Arbeit oder sein lassen meint Maximilian

alle Packages die Maximilian bei NuGet importiert hatte:
* EmguCV
* JsonNet


Training Videos
* https://www.dropbox.com/home/MaximilianSchaller_MA_Videos
* https://www.dropbox.com/scl/fo/ri8jy01q61yrx8u5j1pce/h?rlkey=x5g2e0cyxsvi06c4ctabfdt59&dl=0

## wie dieses Repo?

https://github.com/Sebastian-Schuchmann/AI-Racing-Karts/blob/main/Kart%20Agent.yaml

# Bachelorarbeit Jonas König




https://github.com/jonaskonig/BachelorNN

Unity Projekt:
https://github.com/jonaskonig/carsim


## warum war die Representation der Bloecke so gewaehlt?
x, y, breite und hoehe
wie soll ein NN damit umgehen koennen?
besser waere IMO so:
die 4 coordinaten der 4 ecken (insgesamt 8 werte)

oder 

upper and lower bound, right and left bound of Rectangle (4 values)

Untersuchung von Merlin zeigt, dass die Breite der Bloecke keinen Einfluss auf den Netzwerkoutput hatte


# Reward Function

Interessante Reward function in Trackmania:

Reward ist die Distanz zurueckgelegt in den naechsten 7 Sekunden
https://youtube.com/clip/Ugkxfx5GF0CSNmsVP_s-JZN4RQMePaatG6Vn?si=wptMMB8ytxCX3op8

https://www.youtube.com/watch?v=9juZgQc4D7U&list=WL&index=121



# Merlin Simulation reality gap



# Install instructions

git clone --branch release_20 https://github.com/Unity-Technologies/ml-agents.git


instaled python via Anaconda (this included the h5py library which was difficult to install using pip)

Python Install location:
python -c "import os, sys; print(os.path.dirname(sys.executable))"

C:\Users\gschn\anaconda3


## Emgu.CV

* install visual studio 2019
* create new project
* open NuGet package manager console
    * Install-Package emgu.cv


oder:

* unity use nuget package manager
* this installs to C:\Users\gschn\Desktop\workspace_masterarbeit\master_thesis\carsim\Assets\Packages

## Unity errors

### cvextern not found

DllNotFoundException: cvextern assembly:<unknown assembly> type:<unknown type> member:(null)
Emgu.CV.CvInvoke..cctor () (at <ae22c8657deb40d5ae25c0a930ffb464>:0)
Rethrow as TypeInitializationException: The type initializer for 'Emgu.CV.CvInvoke' threw an exception.
Emgu.CV.MatInvoke..cctor () (at <ae22c8657deb40d5ae25c0a930ffb464>:0)
Rethrow as TypeInitializationException: The type initializer for 'Emgu.CV.MatInvoke' threw an exception.
Emgu.CV.Mat..ctor () (at <ae22c8657deb40d5ae25c0a930ffb464>:0)
ImageRecognitionPipeline.getObstaclePosition (System.Byte[] image) (at Assets/Scripts/ImageRecognitionPipeline.cs:21)
ImageRecognitionPipeline.GetCooridnatesNClosestObstacles (UnityEngine.Vector3 position, System.Byte[] image, System.Int32 n) (at Assets/Scripts/ImageRecognitionPipeline.cs:155)
CarAgent.CollectObservations (Unity.MLAgents.Sensors.VectorSensor sensor) (at Assets/Scripts/CarAgent.cs:164)
Unity.MLAgents.Agent.SendInfoToBrain () (at Library/PackageCache/com.unity.ml-agents@2.0.1/Runtime/Agent.cs:1081)
Unity.MLAgents.Agent.SendInfo () (at Library/PackageCache/com.unity.ml-agents@2.0.1/Runtime/Agent.cs:1326)
Unity.MLAgents.Academy.EnvironmentStep () (at Library/PackageCache/com.unity.ml-agents@2.0.1/Runtime/Academy.cs:573)
Unity.MLAgents.AcademyFixedUpdateStepper.FixedUpdate () (at Library/PackageCache/com.unity.ml-agents@2.0.1/Runtime/Academy.cs:43)

try downloading opencv:
https://sourceforge.net/projects/opencvlibrary/











### duplicate dll's

some dll's are included multiple times for different languages
simply remove them, the unity error message shows the location

Unloading broken assembly Assets/Packages/System.Text.Json.7.0.3/analyzers/dotnet/roslyn4.4/cs/System.Text.Json.SourceGeneration.dll, this assembly can cause crashes in the runtime

## Microsoft.CodeAnalysis.Analyzers.3.3.4
somehow this bullshit always copied itself back into the Assets/Packages folder:

Microsoft.CodeAnalysis.Analyzers.3.3.4
from
C:\Users\gschn\Desktop\workspace_masterarbeit\master_thesis\carsim\Packages
how it reached carsim/Packages is not known



# TODO

ml agents lernen

