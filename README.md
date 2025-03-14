<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Speisekarte</title>
    <style>
        body { 
            font-family: Arial, sans-serif; 
            text-align: center; 
            color: white;
            margin: 0;
            padding: 0;
        }
        .container { 
            max-width: 500px; 
            margin: auto; 
            padding: 20px; 
            background: rgba(0, 0, 0, 0.7); 
            border-radius: 10px;
            position: relative;
            z-index: 1;
        }
        .hidden { display: none; }
        button { margin-top: 10px; padding: 10px; cursor: pointer; position: relative; }
        .selected { background-color: lightgreen; }
        .background {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-size: cover;
            background-position: center;
            z-index: -1;
        }
        .centered {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }
        .info {
            display: none;
            position: absolute;
            background: rgba(0, 0, 0, 0.8);
            color: white;
            padding: 5px;
            border-radius: 5px;
            font-size: 12px;
            width: 200px;
            left: 50%;
            transform: translateX(-50%);
            bottom: 100%;
        }
        .info-icon {
            margin-left: 5px;
            cursor: pointer;
            font-weight: bold;
            display: inline-block;
        }
        .info-icon:hover + .info,
        .info-icon:focus + .info {
            display: block;
        }
    </style>
</head>
<body>
    <div id="background" class="background" style="background-image: url('https://www.merano-suedtirol.it/media/8c5120ba-17c8-440a-bab3-39f10dd2dab9/414_x_414/p=8/tradition-heiraten-heirat-liebe-hochzeit-hochzeitsring-magdalena-patrik-1.jpg');"></div>
    
    <div class="centered" id="nameForm">
        <div class="container">
            <h1>Schön, dass du unsere Einladung erhalten hast!</h1>
            <p>Wir hoffen, dass bei der Speisewahl etwas für dich dabei ist.</p>
            <label for="name">Bitte gib deinen Namen ein:</label>
            <input type="text" id="name" required>
            <button onclick="startSelection()">Weiter</button>
        </div>
    </div>
    
    <div id="menuSelection" class="centered hidden">
        <div class="container">
            <h3>Auswahl Menü</h3>
            
            <h4>Vorspeisen</h4>
            <button onclick="selectItem('Vorspeise', 'Tom Yam', this)">Tom Yam <span class="info-icon">ℹ</span><span class="info">Traditionelle Thai Suppe mit Chili, Limettensaft, Limettenblätter, Zitronengras, Koriander, Galgant Ingwer, Champignons und Tomaten</span></button>
            <button onclick="selectItem('Vorspeise', 'Som Tam', this)">Som Tam <span class="info-icon">ℹ</span><span class="info">Grüner Papayasalat mit Limettensaft, Fischsauce, Chilis, Tomaten und Erdnüssen</span></button>
            <button onclick="selectItem('Vorspeise', 'Sommerrolle', this)">Sommerrolle <span class="info-icon">ℹ</span><span class="info">Reispapierrolle gefüllt mit frischem Gemüse, Glasnudeln und Garnelen</span></button>
            
            <h4>Hauptspeise</h4>
            <button onclick="selectItem('Hauptspeise', 'Pad Thai', this)">Pad Thai <span class="info-icon">ℹ</span><span class="info">Gebratene Reisnudeln mit Ei, Tofu, Erdnüssen und Tamarindensoße</span></button>
            <button onclick="selectItem('Hauptspeise', 'Gai Pad Grapau', this)">Gai Pad Grapau <span class="info-icon">ℹ</span><span class="info">Gebratenes Hühnchen mit Thai-Basilikum, Chili und Knoblauch</span></button>
            <button onclick="selectItem('Hauptspeise', 'Massaman Nüe', this)">Massaman Nüe <span class="info-icon">ℹ</span><span class="info">Mildes Curry mit Rindfleisch, Kartoffeln, Kokosmilch und Erdnüssen</span></button>
            
            <h4>Nachtisch</h4>
            <button onclick="selectItem('Nachtisch', 'Banane im Teigmantel gebacken', this)">Banane im Teigmantel gebacken</button>
            <button onclick="selectItem('Nachtisch', 'Ananas im Teigmantel gebacken', this)">Ananas im Teigmantel gebacken</button>
            
            <h4>Getränke</h4>
            <p>Freie Auswahl</p>
            
            <h4>Bemerkungen und Notizen</h4>
            <textarea id="notes" rows="4" cols="40" placeholder="Hier kannst du Anmerkungen hinterlassen..."></textarea>
            
            <br><br>
            <button onclick="submitSelection()">Bestätigen</button>
        </div>
    </div>
    
    <div id="thankYou" class="centered hidden">
        <div class="container">
            <h2>Vielen Dank!</h2>
            <p>Deine Auswahl wurde gespeichert.</p>
        </div>
    </div>

    <script>
        let selection = {};
        
        function startSelection() {
            const name = document.getElementById('name').value;
            if (name.trim() === '') {
                alert('Bitte gib deinen Namen ein!');
                return;
            }
            document.getElementById('nameForm').style.display = 'none';
            document.getElementById('menuSelection').classList.remove('hidden');
            selection['Name'] = name;
            document.getElementById('background').style.backgroundImage = "url('https://www.my-mauritius.com/fileadmin/user_upload/2023-10_NewsHP-Feuerbach.jpg')";
            window.scrollTo(0, 0);
        }

        function selectItem(category, item, button) {
            const buttons = document.querySelectorAll(`button[onclick^="selectItem('${category}'"]`);
            buttons.forEach(btn => btn.classList.remove('selected'));
            button.classList.add('selected');
            selection[category] = item;
        }
    </script>
</body>
</html>
