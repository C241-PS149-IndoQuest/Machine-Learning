To Load:
from joblib import load
import numpy as np

# Load the vectorizer
tfidf = load('tfidf_vectorizer.joblib')

# Load the cosine similarity matrix
cosine_sim = np.load('cosine_similarity.npy')


To use :
# Assuming you have a function get_recommendations as defined before
destination_name = 'Goa Lawah Temple'
recommendations = get_recommendations(destination_name)

print(f"Recommendations for {destination_name}:")
for i, (name, rating) in enumerate(recommendations.values, 1):
    print(f"{i}. {name} - Rating: {rating}")
