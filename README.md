## Room Finder App - Full Stack Project

### **1. Project Structure:**
```
room-finder-app/
│── backend/  # Flask Backend
│   ├── app.py
│   ├── requirements.txt
│   ├── database.py
│   ├── models.py
│── frontend/  # React Frontend
│   ├── src/
│   │   ├── App.js
│   │   ├── components/
│   │   ├── pages/
│   ├── package.json
│   ├── public/
│── README.md
```

---

## **2. Backend - Flask API (Python)**

### **Backend Setup (Flask)**
- **Install Flask & Dependencies:**
```bash
pip install flask flask-cors flask-sqlalchemy requests
```

- **`backend/app.py` - Flask API**
```python
from flask import Flask, request, jsonify
from flask_cors import CORS

app = Flask(__name__)
CORS(app)

rooms = [
    {"id": 1, "title": "1BHK in Delhi", "location": "Delhi", "price": 10000},
    {"id": 2, "title": "2BHK in Mumbai", "location": "Mumbai", "price": 20000},
    {"id": 3, "title": "PG in Bangalore", "location": "Bangalore", "price": 8000}
]

@app.route("/find_rooms", methods=["GET"])
def find_rooms():
    location = request.args.get("location", "").lower()
    budget = int(request.args.get("budget", 0))
    result = [room for room in rooms if location in room["location"].lower() and room["price"] <= budget]
    return jsonify({"rooms": result})

if __name__ == "__main__":
    app.run(debug=True)
```

- **Run Backend Locally:**
```bash
python backend/app.py
```

---

## **3. Frontend - React App (JavaScript)**

### **Frontend Setup (React)**
- **Install React & Dependencies:**
```bash
npx create-react-app frontend
cd frontend
npm install axios react-router-dom
```

- **`frontend/src/App.js` - React Code**
```javascript
import React, { useState } from "react";
import axios from "axios";

function App() {
    const [location, setLocation] = useState("");
    const [budget, setBudget] = useState("");
    const [rooms, setRooms] = useState([]);

    const fetchRooms = async () => {
        const response = await axios.get(`http://127.0.0.1:5000/find_rooms?location=${location}&budget=${budget}`);
        setRooms(response.data.rooms);
    };

    return (
        <div>
            <h1>Room Finder</h1>
            <input type="text" placeholder="Location" onChange={(e) => setLocation(e.target.value)} />
            <input type="number" placeholder="Budget" onChange={(e) => setBudget(e.target.value)} />
            <button onClick={fetchRooms}>Find Rooms</button>
            <ul>
                {rooms.map((room) => (
                    <li key={room.id}>{room.title} - Rs.{room.price}</li>
                ))}
            </ul>
        </div>
    );
}

export default App;
```

- **Run Frontend Locally:**
```bash
cd frontend
npm start
```

---

### 🎯 **Next Steps:**
1. **Upload this project to GitHub.**
2. **Deploy Backend on Render & Frontend on Vercel.**
3. **Live Room Finder App is ready!** 🚀
4. 
