+++
title = "Veille technologique"
weight = 1
+++

Question envoyée à l’intelligence artificielle : 
```
Explique-moi ce que sont les LLMs locaux, Ollama et le RAG.
```
Réponse :
```
Voici une explication claire et complète — simple, mais assez approfondie pour bien comprendre LLM locaux, Ollama, et le RAG, même si t’es nouveau dans ce monde-là.
________________________________________
✅ 1. C’est quoi un LLM local ?
Un LLM local (Large Language Model local) est un modèle d’intelligence artificielle qui tourne directement sur ton ordinateur, sans envoyer tes données sur Internet.
🔥 Avantages :
•	Confidentialité totale : tout reste sur ton PC.
•	Aucun abonnement : une fois installé, c’est gratuit.
•	Ultra rapide si ton PC est puissant (GPU, RAM).
❗ Inconvénients :
•	Peut demander beaucoup de puissance (VRAM, RAM).
•	Les modèles locaux sont parfois moins puissants que les modèles en ligne comme GPT-5 ou Claude 3.7.
📌 Exemples de LLM locaux :
•	Llama 3
•	Qwen2
•	Mistral 7B / Mixtral
•	Phi-3
Ce sont des modèles que tu peux télécharger (comme un fichier .gguf) et faire tourner chez toi.
________________________________________
✅ 2. C’est quoi Ollama ?
Ollama, c’est une application super simple qui permet :
👉 d’installer,
👉 de gérer,
👉 et de faire tourner des LLM locaux sur ton PC (Windows, Mac, Linux)
➤ Comment ça fonctionne ?
Tu installes Ollama → puis tu peux télécharger un modèle avec une simple commande comme :
ollama run llama3
Et ça marche directement :
tu lui poses des questions, il répond, comme ChatGPT mais en local.
👍 Points forts :
•	Très facile à utiliser.
•	Télécharge automatique les modèles optimisés.
•	Compatible avec plein d’outils (LM Studio, OpenWebUI, VSCode, etc.).
•	Tu peux créer tes propres modèles (modelfile).
🌍 Ollama devient la “référence” actuelle pour les LLM locaux.
________________________________________
✅ 3. C’est quoi le RAG ? (Retrieval Augmented Generation)
Le RAG, c’est une technique qui permet à un LLM de lire tes documents avant de répondre.
🧠 En gros :
1.	Tu donnes des documents (PDF, sites web, notes, Word, etc.).
2.	Un moteur va chercher (retrieval) l’information pertinente.
3.	Le LLM utilise seulement ces infos pour générer (generation) la réponse.
🔥 Pourquoi c’est puissant ?
Parce que ça permet à un modèle moins intelligent (ex : Llama 3 8B) de répondre à des questions de manière aussi précise qu’un grand modèle, tant qu'il a accès aux bons documents.
📌 Exemple concrèt :
Tu donnes tes documents de budgets, règlements, emails, etc.
→ Le LLM peut te faire :
•	Résumés
•	Analyses
•	Rapports
•	Ébauches de mails
•	Réécriture de documents
•	Conseils adaptés à TON organisation
C’est comme avoir ton propre ChatGPT entraîné sur tes documents — mais sans l’entraîner pour vrai.
________________________________________
🎯 Résumé en une ligne
•	LLM local : un gros modèle IA qui roule sur ton PC.
•	Ollama : le logiciel le plus simple pour faire tourner ces modèles.
•	RAG : une technique qui permet à ton IA d’utiliser tes documents pour répondre précisément.
```

# Analyse de la réponse fournie

Après avoir lu la réponse de Chatgpt 5.1 Instant. Nous pouvons constater que la réponse est bien formulée en globalité, le LLM utilise des mots simples et faciles à comprendre, il explique en assez de mots les différentes technologies pour que l’on puisse comprendre la base de ce que c’est un LLM local, Ollama ainsi que le RAG. 

Cependant, je dirais que la réponse reste assez vague, elle explique la base des technologies, mais elle ne va pas beaucoup plus loin que ça dans la technique.

Par exemple, la réponse ne parle pas des limites du RAG, comme des potentielles hallucinations persistantes, c’est-à-dire que le LLM invente des fausses informations, même si ce problème essaie d’être de plus en plus corrigé avec les nouveaux modèles. De plus vu que les LLMS ne pensent pas et qu’ils prédisent statistiquement les mots, ça peut entraîner de mauvaises interprétations.

De plus, en regardant sur différentes pages web, on peut facilement trouver les mêmes informations et même de façons plus développées. Par exemple, sur la page Wikipédia « Retrieval-Augmented Generation », on explique le fonctionnement interne du RAG : la page parle des embeddings (vecteurs numériques) qui transforment les mots/paragraphes en suite de nombres. Ce qui facilite l’intelligence artificielle à comprendre. On parle aussi des retrievers qui servent à retrouver les documents les plus pertinents en fonction de la question qui lui a été posée ainsi que d’autres mécanismes internes utilisés par le RAG.

Les différentes sources fournissent des informations beaucoup plus développées sur les LLM que la réponse reçue par ChatGpt. Dans l’article : « What are LLMs, Local LLMs and RAG? » On nous apprend comment construire et entraîner un modèle : en l’entraînant comme on l’a aussi vu en cours (machine learning), ou bien avec de la collecte de données.  

En comparaison à un moteur de recherche comme Google, la réponse de ChatGpt est très facile à lire et à comprendre, comme je l’ai dit un peu plus haut. La réponse est plus ou moins la même si on pose la question à Gemini. Pour une personne qui n’en saurait rien sur le sujet et qui aimerait simplement faire une courte recherche sur le sujet, je pense que cela suffirait. Mais si on veut s’approfondir un peu plus sur le sujet, avec une recherche Google nous pourrions directement tomber sur différents sites web ou vidéos youtubes qui fourniraient des réponses plus développées et plus techniques.

Pour conclure, il n’y a pas un site exactement qui possède toutes les informations concernant les LLM, Ollama ainsi que le RAG, mais en faisant quelques petites recherches, nous pouvons rapidement trouver des informations intéressantes et plus poussées sur le sujet que la simple recherche sur ChatGpt ou bien Gemini. Il y a aussi des vidéos complètes qui expliquent le sujet de manière assez claire.

## Sources : 

**Comment les LLM marchent** 
- https://www.youtube.com/watch?v=5sLYAQS9sWQ&t=2s

**Explication détaillée de llama3.1**
- https://ai.meta.com/blog/meta-llama-3-1/ 

**Explication du RAG**
- https://en.wikipedia.org/wiki/Retrieval-augmented_generation 

**Explication LLM, Local LLM et RAG**
- https://medium.com/@arjunrao87/what-are-llms-local-llms-and-rag-0198868f8657

##### Vidéos youtubes : 

**Explication du fonctionnement des LLM**
- https://www.youtube.com/watch?v=5sLYAQS9sWQ&t=2s 

**C’est quoi un RAG**
- https://www.youtube.com/watch?v=T-D1OfcDW1M 

**C’est quoi llama3.1**
- https://youtu.be/8c2LnKNoSmg