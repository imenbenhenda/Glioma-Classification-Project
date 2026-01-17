### Étapes pour créer une application Streamlit

1. **Installer Streamlit** : Si vous ne l'avez pas encore fait, installez Streamlit en utilisant pip.

   ```bash
   pip install streamlit
   ```

2. **Créer un fichier Python** : Créez un fichier Python, par exemple `app.py`.

3. **Écrire le code de l'application** : Voici un exemple de code pour une application Streamlit qui permet de charger un fichier CSV et d'afficher des statistiques de base.

   ```python
   import streamlit as st
   import pandas as pd
   import numpy as np
   import matplotlib.pyplot as plt

   # Titre de l'application
   st.title("Analyse de données avec Streamlit")

   # Chargement du fichier CSV
   uploaded_file = st.file_uploader("Choisissez un fichier CSV", type="csv")

   if uploaded_file is not None:
       # Lire le fichier CSV
       df = pd.read_csv(uploaded_file)

       # Afficher les premières lignes du DataFrame
       st.write("Aperçu des données :")
       st.dataframe(df.head())

       # Afficher des statistiques descriptives
       st.write("Statistiques descriptives :")
       st.write(df.describe())

       # Sélectionner une colonne pour le graphique
       column = st.selectbox("Sélectionnez une colonne pour le graphique", df.columns)

       # Afficher un histogramme de la colonne sélectionnée
       st.write(f"Histogramme de {column} :")
       plt.hist(df[column], bins=30, alpha=0.7, color='blue')
       plt.xlabel(column)
       plt.ylabel('Fréquence')
       st.pyplot(plt)

       # Option pour afficher une corrélation
       if st.checkbox("Afficher la matrice de corrélation"):
           st.write("Matrice de corrélation :")
           correlation = df.corr()
           st.write(correlation)

           # Afficher la matrice de corrélation sous forme de heatmap
           plt.figure(figsize=(10, 8))
           plt.imshow(correlation, cmap='coolwarm', interpolation='none')
           plt.colorbar()
           plt.xticks(range(len(correlation.columns)), correlation.columns, rotation=90)
           plt.yticks(range(len(correlation.columns)), correlation.columns)
           st.pyplot(plt)

   ```

4. **Exécuter l'application** : Dans le terminal, exécutez la commande suivante pour lancer votre application Streamlit.

   ```bash
   streamlit run app.py
   ```

5. **Accéder à l'application** : Ouvrez votre navigateur et allez à l'adresse `http://localhost:8501` pour voir votre application en action.

### Fonctionnalités de l'application

- **Chargement de fichiers CSV** : Les utilisateurs peuvent télécharger leurs propres fichiers CSV pour analyse.
- **Aperçu des données** : Affiche les premières lignes du DataFrame pour donner un aperçu des données.
- **Statistiques descriptives** : Affiche des statistiques de base sur les données.
- **Visualisation** : Permet aux utilisateurs de sélectionner une colonne et d'afficher un histogramme.
- **Matrice de corrélation** : Option pour afficher la matrice de corrélation des données.

### Personnalisation

Vous pouvez personnaliser cette application en ajoutant d'autres fonctionnalités, comme des filtres, des graphiques supplémentaires, ou même des modèles de machine learning. Streamlit offre une grande flexibilité pour créer des applications interactives et visuellement attrayantes.