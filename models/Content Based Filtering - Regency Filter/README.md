1. Load the saved components from this file:
import joblib

# Load the TF-IDF vectorizer
tfidf = joblib.load('tfidf_vectorizer.joblib')

# Load the TF-IDF matrix
tfidf_matrix = joblib.load('tfidf_matrix.joblib')

# Load the cosine similarity matrix
cosine_sim = joblib.load('cosine_similarity.joblib')


2. Ensure data frame structure 
Make sure that the DataFrame (df) you are using in the new environment has the same structure, particularly the columns and their ordering as expected by the recommendation function. If the DataFrame is not present in the new environment, you will need to recreate it or load it from a saved state.

3. Reusing the recommendation function
You can directly use the get_recommendations function if it's defined in the environment. If not, redefine it as shown in your previous code snippet, making sure it uses the loaded cosine_sim:
import pandas as pd  # Ensure pandas is imported if using DataFrame

def get_recommendations(destination_name, cosine_sim=cosine_sim):

    # Get the index of the destination that matches the name
    idx = df[df['Destination Name'] == destination_name].index[0]

    # Get the pairwise similarity scores of all destinations with that destination
    sim_scores = list(enumerate(cosine_sim[idx]))

    # Sort the destinations based on similarity scores
    sim_scores = sorted(sim_scores, key=lambda x: x[1], reverse=True)

    # Get the scores of the 10 most similar destinations
    sim_scores = sim_scores[1:11]

    # Get the destination indices
    destination_indices = [i[0] for i in sim_scores]

    # Return the top 10 most similar destinations
    return df[['Destination Name', 'Rating']].iloc[destination_indices]

# Example usage
destination_name = 'Pura Ulun Danu Bratan'
recommendations = get_recommendations(destination_name)

print(f"Recommendations for {destination_name}:")
for i, (name, rating) in enumerate(recommendations.values, 1):
    print(f"{i}. {name} - Rating: {rating}")
