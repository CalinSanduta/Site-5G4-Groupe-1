+++
title = "Atelier"
weight = 3
+++

## Atelier correcteur de grammaire 

#### Étape 1 : Préparation des fichiers 

Pour commencer, il faudra installer ollama et essayer de générer une réponse avec llama3.1.

Commencez par taper cette commande :
```
sudo apt update
```
Ensuite, ouvrez le terminal et taper la commande suivante, pour installer Ollama : 
```
curl -fsSL https://ollama.com/install.sh | sh
```
Ensuite créez un fichier dans lequel vous mettez :
```
Import ollama
response = llama.generate(model= "llama3.1", prompt="Explique-moi ce qu'est un LLM local. En deux phrases.")
print(response.reponse)
```
Réponse :
```
Un modèle de langage large (LLM) local est une copie d'un grand modèle de langage, comme ceux développés par les géants de la technologie, qui a été déployé sur un appareil ou un système spécifique, telle qu’un serveur en ligne privée ou un ordinateur personnel. Cela permet à des organisations et des individus de bénéficier d'un traitement avancé du langage naturel sans avoir recours aux services en ligne, qui peuvent présenter des risques liés à la confidentialité et à l'efficacité.
```

Voilà, maintenant vous venez de mettre en place ollama, llama3.1 et fait en sorte d’y générer une réponse. 

## Début de l’atelier (correcteur de grammaire)

Maintenant nous allons passer à la partie un peu plus avancée. Voici la structure que votre projet devra avoir : 
 
Vous devez créer un fichier `requirements.txt` que vous utiliserez ensuite pour installer vos dépendances : 
```
langchain
langchain_ollama
langchain-community
PyPDF2
chromadb
llama-index
tqdm
pydantic
requests
```

Dans `text_input/texte_utilisateur.txt` :
```
Les élève qui étudient à Paris mange des pomme et des croissant chaque matin, mais parfois il oublie de faire ses devoirs.
```

Ensuite, il faut aller dans le `venv` et installer le tout :
```
source venv /bin /activate
pip install -r requirements.txt
```

## Code de l’atelier 
Dans `utils/analyse_pdf.py` vous devez insérer cela : 
```
import PyPDF2

def extraire_regles_pdf(pdf_path):
    texte = ""
    with open(pdf_path, "rb") as f:
        reader = PyPDF2.PdfReader(f)
        for page in reader.pages:
            texte += page.extract_text()
    return texte
```
Dans `utils/ragnlp.py` insérez :
```
from langchain_ollama import OllamaEmbeddings
from langchain_text_splitters import RecursiveCharacterTextSplitter
from langchain_community.vectorstores import Chroma


def appliquer_rag(regles_pdf: str):

    # Split du texte en petits morceaux
    splitter = RecursiveCharacterTextSplitter(chunk_size=500, chunk_overlap=50)
    chunks = splitter.split_text(regles_pdf)

    # Embeddings OLlama
    embeddings = OllamaEmbeddings(model="llama3.1")

    # Création base vectorielle avec Chroma
    vecteur_store = Chroma.from_texts(chunks, embedding=embeddings)

    # Création du retriever
    retriever = vecteur_store.as_retriever(search_kwargs={"k": 3})

    return retriever
```

Dans `utils/correction_automatique.py` : 
```
from langchain_ollama import ChatOllama

def appliquer_correction_automatique(texte_utilisateur: str, retriever):
    """
    Corrige seulement les fautes visibles dans le texte utilisateur.
    Ne modifie jamais le sens.
    Ne reformule jamais.
    Ne propose jamais d'alternatives.
    Utilise seulement les règles du PDF via RAG.
    """

    # Recuperation des regles via le RAG
    regles = retriever.invoke(texte_utilisateur)
    regles_text = "\n".join([doc.page_content for doc in regles])

    llm = ChatOllama(model="llama3.1")

    prompt = f"""
TU ES UN CORRECTEUR GRAMMATICAL STRICT ET NON CRÉATIF.

Voici les règles extraites du PDF :
--------------------
{regles_text}
--------------------

Voici le texte à corriger (NE CHANGE PAS LE SENS) :
--------------------
{texte_utilisateur}
--------------------

RÈGLES ABSOLUES :

Tu ne dois pas ajouter d'introduction, pas de phrases avant ou après.

Tu ne dois pas réécrire la phrase autrement que pour corriger l’orthographe/grammaire.
Tu ne dois pas proposer d'alternatives ou reformulations.
Tu ne dois pas inventer des erreurs.
Tu ne dois pas modifier la structure ni la ponctuation SAUF si c’est une faute évidente.
Si plusieurs corrections possibles existent, garde LA PLUS SIMPLE.
Si une règle n'est PAS dans le PDF → écris : "règle absente du PDF".
Tu dois répondre STRICTEMENT dans le format demandé ci-dessous.
FORMAT DE SORTIE OBLIGATOIRE (ne change rien au format) :

TEXTE CORRIGÉ :
(le texte corrigé ici — une seule version)

ERREURS DÉTECTÉES :

    (erreur originale) → (correction) → (règle PDF utilisée ou "règle absente du PDF")

"""

    resultat = llm.invoke(prompt)
    return resultat.content
```
Dans `main.py` :
```
import utils.analyse_pdf as analyse_pdf
import utils.correction_automatique as correction
import utils.ragnlp as rag


def main():
    print("Chargement du texte utilisateur...")
    with open("text_input/texte_utilisateur.txt", "r", encoding="utf-8") as f:
        texte_utilisateur = f.read()

    print("Extraction des règles PDF...")
    regles_pdf = analyse_pdf.extraire_regles_pdf("pdf_rules/regles_correction.pdf")

    print("Création du retriever RAG...")
    retriever = rag.appliquer_rag(regles_pdf)

    print("Application de la correction...")
    resultat = correction.appliquer_correction_automatique(texte_utilisateur, retriever)

    print("\n      RÉSULTAT FINAL      \n")
    print(resultat)
    print("\n--------------------------\n")


if __name__ == "__main__":
    main()
```

Vous recevrez une réponse de ce type : 
```
TEXTE CORRIGÉ :

Les élèves qui étudient à Paris mangent des pommes et des croissants chaque matin, mais parfois il oublie de faire ses devoirs.

ERREURS DÉTECTÉES :

"élève" → "élèves" (règle absente du PDF)
"qui" (pas "qui étudient", mais seulement "qui") : les élèves qui étudient à Paris... (Utilisez "que" lorsque le pronom relatif est complément d'objet direct. Par exemple : Le livre que j'ai lu est intéressant.)
"mange des pomme et des croissant" → "mangent des pommes et des croissants" (règle absente du PDF)
"il oublie de faire ses devoirs" (correct en tant que phrase, mais la ponctuation n'est pas évidemment fautive. Toutefois, le manque d'ajout de virgules dans une liste implique un non-respect des règles de ponctuations : il oublie de faire ses devoirs, alors qu'une virgule serait nécessaire : mais parfois il oublie de faire ses devoirs, alors que...)
"mange" → "mangent" (règle absente du PDF)
```

Félicitations, vous venez de crée votre tout premier programme qui sert à corriger le grammaire grâce à un modèle d’intelligence artificielle, ainsi qu’à un RAG qui permet à l’intelligence de pouvoir accéder à un pdf, pour permettre à l'intelligence d'avoir des meilleures connaissances sur la matière.