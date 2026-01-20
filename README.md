# Livraison-
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Pedidos-Dessa | Livraison Rapide</title>
    <style>
        :root { --primary: #e63946; --dark: #1d3557; --light: #f1faee; }
        body { font-family: sans-serif; background: var(--light); margin: 0; padding: 15px; }
        header { background: var(--dark); color: white; padding: 20px; text-align: center; border-radius: 10px; margin-bottom: 20px; }
        .card { background: white; padding: 15px; border-radius: 10px; box-shadow: 0 2px 5px rgba(0,0,0,0.1); margin-bottom: 15px; display: flex; justify-content: space-between; align-items: center; }
        .product-info h3 { margin: 0; color: var(--dark); }
        .product-info p { margin: 5px 0; color: #666; font-weight: bold; }
        button { background: var(--primary); color: white; border: none; padding: 10px 15px; border-radius: 5px; cursor: pointer; }
        #cart { background: var(--dark); color: white; padding: 20px; border-radius: 10px; position: sticky; bottom: 10px; display: none; }
        input { width: 100%; padding: 10px; margin-top: 10px; border-radius: 5px; border: 1px solid #ccc; box-sizing: border-box; }
    </style>
</head>
<body>

<header>
    <h1>Pedidos-Dessa</h1>
    <p>Jacquet Toto &bull; Puits Blain</p>
</header>

<div id="app">
    <div class="card">
        <div class="product-info">
            <h3>Sac de Riz (25kg)</h3>
            <p>Prix: 2500 HTG</p>
        </div>
        <button onclick="addToCart('Riz 25kg', 2500)">Ajouter</button>
    </div>

    <div class="card">
        <div class="product-info">
            <h3>Huile (1 Gallon)</h3>
            <p>Prix: 1200 HTG</p>
        </div>
        <button onclick="addToCart('Huile 1Gal', 1200)">Ajouter</button>
    </div>

    <div class="card">
        <div class="product-info">
            <h3>Caisse d'Eau</h3>
            <p>Prix: 500 HTG</p>
        </div>
        <button onclick="addToCart('Eau Caisse', 500)">Ajouter</button>
    </div>
</div>

<div id="cart">
    <h3>Ma Commande</h3>
    <div id="cart-items"></div>
    <hr>
    <p>Total: <span id="total">0</span> HTG</p>
    <input type="text" id="address" placeholder="Adresse exacte (ex: Puits Blain, Rue X)">
    <button style="width:100%; margin-top:10px; background: #25D366;" onclick="sendWhatsApp()">Commander via WhatsApp</button>
</div>

<script>
    let cart = [];
    let total = 0;

    function addToCart(name, price) {
        cart.push({name, price});
        total += price;
        updateUI();
    }

    function updateUI() {
        const cartDiv = document.getElementById('cart');
        const itemsDiv = document.getElementById('cart-items');
        const totalSpan = document.getElementById('total');
        
        cartDiv.style.display = 'block';
        itemsDiv.innerHTML = cart.map(item => `<div>${item.name}</div>`).join('');
        totalSpan.innerText = total;
    }

    function sendWhatsApp() {
        const address = document.getElementById('address').value;
        if(!address) return alert("Précisez l'adresse de livraison");
        
        let message = `*Nouvelle Commande Pedidos-Dessa*%0A`;
        message += `--------------------------%0A`;
        cart.forEach(item => message += `- ${item.name}%0A`);
        message += `--------------------------%0A`;
        message += `*Total:* ${total} HTG%0A`;
        message += `*Lieu:* ${address}`;
        
        // REMPLACE LE NUMÉRO CI-DESSOUS PAR LE TIEN (Format international sans le +)
        const myNumber = "50938573192"; 
        window.open(`https://wa.me/${myNumber}?text=${message}`);
    }
</script>

</body>
</html>
