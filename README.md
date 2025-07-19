Le projet portait sur l’identification automatisée des collemboles (collembolans) à l’aide de méthodes de deep learning. 🧠
Ces micro-organismes présentent un véritable défi : leur taille infime, des différences morphologiques parfois très subtiles et l’usage obligatoire de la microscopie 🔬 compliquent grandement leur reconnaissance.

Nous disposions de 1 117 images annotées, chacune associée à des bounding boxes au format YOLO+ et à quatre jeux d’étiquettes fournis par des experts, variant de 0 à 8 selon l’espèce. Ces annotations souffraient de plusieurs biais et contradictions. 📊

Nos objectifs :

Sur la base de test non étiquetée, prédire les classes de collemboles et mesurer la performance via le F1-macro sur la plateforme Kaggle.

À partir des annotations conflictuelles du jeu d’entraînement, déterminer les véritables labels de chaque espèce.

Principaux challenges :

Grande hétérogénéité des images (résolution, qualité et conditions d’éclairage variables).

Disparités entre les annotations des experts, rendant le jeu de données d’entraînement bruité.

Prédominance de la classe majoritaire (0 – « autres »), difficile à distinguer visuellement des espèces ciblées.

Mauvaises annotations YOLO+ : certaines images contenaient des spécimens alors qu’elles étaient supposées ne représenter que le “fond”.
