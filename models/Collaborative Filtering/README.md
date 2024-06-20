1. To load:
# Load the SVD model from a file
with open('svd_model.pkl', 'rb') as f:
    loaded_model = pickle.load(f)

2. Using the Loaded Model:
Once the model is loaded, you can use it in the same way as before. For example, if you want to get recommendations for a user, you can call the get_top_n_recommendations function:

# Example usage: Get top 10 recommendations for a user with ID 2
user_id = 2
recommendations = get_top_n_recommendations(loaded_model, user_id)

print(f"Top 10 Recommendations for User {user_id}:")
for i, (name, rating) in enumerate(recommendations.values, 1):
    print(f"{i}. {name} - Rating: {rating}")

