from flask import Flask, request, jsonify, redirect
import string
import random

app = Flask(__name__)

# In-memory database (dictionary) to store short codes
url_mapping = {}

# Function to generate a random short code
def generate_short_code(length=6):
    characters = string.ascii_letters + string.digits
    return ''.join(random.choice(characters) for _ in range(length))

# API endpoint to shorten a long URL
@app.route('/shorten', methods=['POST'])
def shorten_url():
    data = request.get_json()
    long_url = data.get("longUrl")

    if not long_url:
        return jsonify({"error": "Please provide a URL"}), 400

    short_code = generate_short_code()
    url_mapping[short_code] = long_url

    return jsonify({"shortUrl": f"http://localhost:5000/{short_code}"})

# Redirect route for short URL
@app.route('/<short_code>')
def redirect_url(short_code):
    long_url = url_mapping.get(short_code)
    if long_url:
        return redirect(long_url)
    return jsonify({"error": "Not found"}), 404

if __name__ == '__main__':
    app.run(debug=True)
