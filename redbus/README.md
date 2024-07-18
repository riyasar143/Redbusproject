


import streamlit as st
import sqlite3

# Connect to SQLite database
conn = sqlite3.connect('redbus_data.db')
c = conn.cursor()

# Streamlit application code
st.title('Redbus Data Analysis')

# Add filters
bus_types = ['Sleeper', 'Seater', 'AC', 'Non-AC']
selected_bus_type = st.multiselect('Select bus types', bus_types)

# Query data based on filters
query = "SELECT * FROM bus_routes WHERE bustype IN ({seq})".format(seq=','.join(['?']*len(selected_bus_type)))
filtered_data = c.execute(query, selected_bus_type).fetchall()

# Display filtered data
for row in filtered_data:
    st.write(row)

# Close database connection
conn.close()