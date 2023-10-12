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

## Send data from python to Unity (Socket)
https://www.youtube.com/watch?v=Dm0CiAiZk14

https://www.youtube.com/watch?v=fGHde1h_vaA


## JetBot Roboter

https://developer.nvidia.com/embedded/learn/jetbot


# Notizen zu Maddi97 Masterarbeit
https://github.com/Maddi97/master_thesis

warum sind hier nur 7 Python Skripte? (alle zur Analyse der Ergebnisse)
https://github.com/search?q=repo%3AMaddi97%2Fmaster_thesis%20.py&type=code



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

