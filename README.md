# Travel Memory

`.env` file to work with the backend after creating a database in mongodb: 

```
MONGO_URI='mongodb+srv://Swetatpatil:Rudyredindian2507@Swetapatil.nlqpeax.mongodb.net/?appName=Swetapatil'
PORT=3001
```

Data format to be added: 

```json
{
    "tripName": "Road Trip to Karnataka",
    "startDateOfJourney": "24-12-2025",
    "endDateOfJourney": "02-01-2026",
    "nameOfHotels":"Club Mahindra",
    "placesVisited":"Mysore, Humpi, Otty, Coorg",
    "totalCost": 60000,
    "tripType": "backpacking",
    "experience": "awesome and peaceful experience",
    "image": "https://www.bing.com/images/search?q=virupaksha+temple+hampi&form=HDRSC3&first=1",
    "shortDescription":"Road Trips are the best choice, its one of my best trip.",
    "featured": true
}
```


For frontend, you need to create `.env` file and put the following content (remember to change it based on your requirements):
```bash
REACT_APP_BACKEND_URL=http://localhost:3001
```