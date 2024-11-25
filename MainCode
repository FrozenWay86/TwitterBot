import tweepy
import os
import random
import json

# Clés et jetons d'accès
API_KEY = os.getenv('API_KEY')
API_SECRET_KEY = os.getenv('API_SECRET_KEY')
ACCESS_TOKEN = os.getenv('ACCESS_TOKEN')
ACCESS_TOKEN_SECRET = os.getenv('ACCESS_TOKEN_SECRET')

# Authentification
auth = tweepy.OAuthHandler(API_KEY, API_SECRET_KEY)
auth.set_access_token(ACCESS_TOKEN, ACCESS_TOKEN_SECRET)
api = tweepy.API(auth)

# Liste de messages prédéfinis
messages = [
    "Message 1: N'oubliez pas de sourire aujourd'hui ! 😊",
    "Message 2: Une nouvelle journée, une nouvelle opportunité.",
    "Message 3: Croyez en vous, tout est possible ! 💪",
    "Message 4: Prenez un moment pour respirer profondément. 🌬️",
    "Message 5: Partagez une bonne nouvelle aujourd'hui. 📰",
]

# Fichier pour garder trace des messages publiés
TRACK_FILE = "published_messages.json"

# Charger les messages publiés précédemment
def load_published_messages():
    if os.path.exists(TRACK_FILE):
        with open(TRACK_FILE, 'r') as file:
            return json.load(file)
    return []

# Enregistrer les messages publiés
def save_published_messages(published_messages):
    with open(TRACK_FILE, 'w') as file:
        json.dump(published_messages, file)

# Fonction principale
def post_random_message():
    published_messages = load_published_messages()
    remaining_messages = [msg for msg in messages if msg not in published_messages]

    if not remaining_messages:
        print("Tous les messages ont été publiés. Réinitialisation de la liste.")
        published_messages = []
        remaining_messages = messages

    # Choisir un message aléatoire
    message_to_post = random.choice(remaining_messages)

    # Publier le message sur Twitter
    api.update_status(message_to_post)
    print(f"Publié : {message_to_post}")

    # Mettre à jour les messages publiés
    published_messages.append(message_to_post)
    save_published_messages(published_messages)

# Appeler la fonction
if __name__ == "__main__":
    post_random_message()
