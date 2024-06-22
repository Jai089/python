import sqlite3

# Create the Database and Tables
def create_tables():
    conn = sqlite3.connect('website_data.db')
    cursor = conn.cursor()

    cursor.execute('''
        CREATE TABLE IF NOT EXISTS Users (
            user_id INTEGER PRIMARY KEY,
            username TEXT NOT NULL,
            email TEXT NOT NULL
        )
    ''')

    cursor.execute('''
        CREATE TABLE IF NOT EXISTS Pages (
            page_id INTEGER PRIMARY KEY,
            url TEXT NOT NULL,
            title TEXT NOT NULL,
            content TEXT NOT NULL
        )
    ''')

    cursor.execute('''
        CREATE TABLE IF NOT EXISTS Visits (
            visit_id INTEGER PRIMARY KEY,
            user_id INTEGER,
            page_id INTEGER,
            visit_time TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
            FOREIGN KEY (user_id) REFERENCES Users (user_id),
            FOREIGN KEY (page_id) REFERENCES Pages (page_id)
        )
    ''')

    conn.commit()
    conn.close()

# Add, Remove, and Modify Data functions
def add_user(username, email):
    conn = sqlite3.connect('website_data.db')
    cursor = conn.cursor()
    cursor.execute('INSERT INTO Users (username, email) VALUES (?, ?)', (username, email))
    conn.commit()
    conn.close()

def add_page(url, title, content):
    conn = sqlite3.connect('website_data.db')
    cursor = conn.cursor()
    cursor.execute('INSERT INTO Pages (url, title, content) VALUES (?, ?, ?)', (url, title, content))
    conn.commit()
    conn.close()

def add_visit(user_id, page_id):
    conn = sqlite3.connect('website_data.db')
    cursor = conn.cursor()
    cursor.execute('INSERT INTO Visits (user_id, page_id) VALUES (?, ?)', (user_id, page_id))
    conn.commit()
    conn.close()

# Query and Organize Data functions
def get_all_users():
    conn = sqlite3.connect('website_data.db')
    cursor = conn.cursor()
    cursor.execute('SELECT * FROM Users')
    users = cursor.fetchall()
    conn.close()
    return users

def get_all_pages():
    conn = sqlite3.connect('website_data.db')
    cursor = conn.cursor()
    cursor.execute('SELECT * FROM Pages')
    pages = cursor.fetchall()
    conn.close()
    return pages

def get_user_visits(user_id):
    conn = sqlite3.connect('website_data.db')
    cursor = conn.cursor()
    cursor.execute('''
        SELECT Pages.url, Pages.title, Visits.visit_time 
        FROM Visits 
        JOIN Pages ON Visits.page_id = Pages.page_id 
        WHERE Visits.user_id = ?
    ''', (user_id,))
    visits = cursor.fetchall()
    conn.close()
    return visits

# Main Function to Demonstrate Usage
if __name__ == "__main__":
    # Create tables if they do not exist
    create_tables()

    # Add users
    add_user('alice', 'alice@example.com')
    add_user('bob', 'bob@example.com')

    # Add pages
    add_page('http://example.com/home', 'Home', 'Welcome to the homepage!')
    add_page('http://example.com/about', 'About', 'About us page.')

    # Log visits
    add_visit(1, 1)  # Alice visits Home
    add_visit(2, 2)  # Bob visits About

    # Display data for demonstration
    print("All Users:")
    print(get_all_users())

    print("\nAll Pages:")
    print(get_all_pages())

    print("\nAlice's Visits:")
    print(get_user_visits(1))  # Alice's visits
