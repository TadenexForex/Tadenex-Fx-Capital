
from flask import Flask, render_template, request, redirect, url_for
import pandas as pd
import numpy as np

app = Flask(__name__)
app.secret_key = 'secret'

# Load data
df = pd.read_csv('investment_data.csv')

# Define routes
@app.route('/')
def home():
    return render_template('home.html')

@app.route('/login', methods=['GET', 'POST'])
def login():
    if request.method == 'POST':
        username = request.form['username']
        password = request.form['password']

        if username == 'admin' and password == 'admin':
            session['logged_in'] = True
            return redirect(url_for('recommend'))
        else:
            return render_template('login.html', error=True)

    return render_template('login.html', error=False)

@app.route('/logout')
def logout():
    session['logged_in'] = False
    return redirect(url_for('home'))

@app.route('/recommend', methods=['GET', 'POST'])
def recommend():
    if not session.get('logged_in'):
        return redirect(url_for('login'))

    # Get user input
    age = int(request.form['age'])
    income = float(request.form['income'])
    risk_tolerance = request.form['risk_tolerance']

    # Filter data based on user input
    filtered_df = df[(df['Age'] <= age) & (df['Income'] <= income) & (df['Risk Tolerance'] == risk_tolerance)]

    # Calculate recommended investment based on filtered data
    recommended_investment = filtered_df.groupby('Investment Type')['Expected Return'].max().idxmax()

    # Render recommendation template with recommended investment
    return render_template('recommendation.html', investment=recommended_investment)

if __name__ == '__main__':
    app.run(debug=True)

  <html>
    <header>
      <h1>Tadenex Forex Capital</h1>
      <nav>
        <ul>
          <li><a href="#">Home</a></li>
          <li><a href="#">About Us</a></li>
          <li><a href="#">Services</a></li>
          <li><a href="#">Contact Us</a></li>
        </ul>
      </nav>
    </header>
    <main>
      <section>
        <h2>About Us</h2>
<html>
   <head>
        <p>Welcome to Tadenex Forex Capital, your trusted partner in the foreign exchange market. We provide reliable and efficient forex trading services to help you achieve your investment goals. Our team of experts is dedicated to delivering top-notch financial solutions to our clients.</p>
      </section>
      <section>
        <h2>Services</h2>
        <ul>
          <li>Forex Trading</li>
          <li>Portfolio Management</li>
          <li>Investment Advisory</li>
          <li>Risk Management</li>
        </ul>
      </section>
      <section>
        <h2>Contact Us</h2>
        <form>
          <label for="name">Name:</label>
          <input type="text" id="name" name="name"><br>
          <label for="email">Email:</label>
          <input type="email" id="email" name="email"><br>
          <label for="message">Message:</label>
          <textarea id="message" name="message"></textarea><br>
          <input type="submit" value="Submit">
        </form>
      </section>
    </main>
    <footer>
      <p>&copy; 2023 Tadenex Forex Capital. All rights reserved.</p>
    </footer>
  </body>
</html>
 'index.html'
<html>
  <head>
    <title>Tadenex Forex Capital - Home</title>
    <link rel="stylesheet" type="text/css" href="style.css">
  </head>
  <body>
    <nav>
      <ul>
        <li><a href="index.html">Home</a></li>
        <li><a href="about.html">About Us</a></li>
        <li><a href="contact.html">Contact Us</a></li>
        <li><a href="login.html">Login</a></li>
      </ul>
    </nav>
    <header>
      <h1>Tadenex Forex Capital</h1>
      <p>Welcome to Tadenex Forex Capital, your trusted partner in investment.</p>
    </header>
    <main>
      <h2>Our Investment Packages</h2>
      <ul>
        <li>
          <h3>Starter</h3>
          <p>Investment: $1,000 - $9,999</p>
          <p>ROI: 5%</p>
          <p>Duration: 30 days</p>
        </li>
        <li>
          <h3>Advanced</h3>
          <p>Investment:$100-1000$
200$-2000$
300-3000$
400$-4000$
500$-5000$
600$-6000$
 $10,000 - $49,999</p>
          <p>ROI: 7.5%</p>
          <p>Duration: 60 days</p>
        </li>
        <li>
          <h3>Professional</h3>
          <p>Investment: $50,000 - $249,999</p>
          <p>ROI: 10%</p>
          <p>Duration: 90 days</p>
        </li>
        <li>
          <h3>Expert</h3>
          <p>Investment: $250,000 - $1,000,000</p>
          <p>ROI: 15%</p>
          <p>Duration: 180 days</p>
        </li>
      </ul>
      <a href="login.html" class="cta-button">Start Investing Now</a>
    </main>
    <footer>
      <p>&copy; 2023 Tadenex Forex Capital. All rights reserved.</p>
    </footer>
  </body>
</html>

'About.html'
<html>
  <head>
    <title>Tadenex Forex Capital - About Us</title>
    <link rel="stylesheet" type="text/css" href="style.css">
  </head>
  <body>
    <nav>
      <ul>
        <li><a href="index.html">Home</a></li>
        <li><a href="about.html">About Us</a></li>
        <li><a href="contact.html">Contact Us</a></li>
        <li><a href="login.html">Login</a></li>
      </ul>
    </nav>
    <header>
      <h1>About Us</h1>
      <p>Tadenex Forex Capital is a leading investment company that specializes in Forex trading. We offer our clients innovative investment solutions that deliver high returns with minimal risk.</p>
    </header>
    <main>
      <h2>Our Mission</h2>
      <p>Our mission is to help our clients achieve their financial goals by providing them with the best investment opportunities in the market
