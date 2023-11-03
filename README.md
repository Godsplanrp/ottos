
<html>
<head>
  <title>Menu Calculator</title>
    <style>
    body {
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      height: 250vh;
      text-align: center;
    }
	.total-box {
		display: flex;
		justify-content: center; /* Center horizontally */
		align-items: center; /* Center vertically */
		margin-top: 20px;
	}}
	
	 .calculate-button {
      width: 150px; /* Adjust the desired width */
      height: 50px; /* Adjust the desired height */
    }
	
	.submit-button {
      width: 150px; /* Adjust the desired width */
      height: 40px; /* Adjust the desired height */
    }
	
	.reset-button {
      width: 150px; /* Adjust the desired width */
      height: 30px; /* Adjust the desired height */
    }
    
    h1 {
      margin-bottom: 20px;
    }
    
    h2 {
      margin-top: 20px;
    }
	
	h3 {
      border: 1px solid black; /* Adjust the border style as needed */
      padding: 5px; /* Add padding to create space around the heading */
    }
    
    .menu-items {
      display: flex;
      flex-direction: column;
      align-items: flex-start;
      gap: 10px;
      margin-bottom: 10px;
    }
    
    .menu-items div {
      display: flex;
      align-items: center;
    }
    
    .total-box {
      display: flex;
      justify-content: flex-end;
      align-self: Center;
      margin-top: 20px;
    }
    
    .button-container {
      display: flex;
      gap: 10px;
      margin-top: 20px;
    }
	
	.menu-items div img {
      width: 50px; /* Adjust the desired width */
      height: 50px; /* Adjust the desired height */
      margin-left: 10px; /* Add margin as per your preference */
    }
    {
    button {
      margin-top: 20px;
	}}}}}}
  </style>
  <script>
    function calculateTotal() {
    var total = 0;
    var checkboxes = document.querySelectorAll('input[type="checkbox"]:checked');

    checkboxes.forEach(function(checkbox) {
      var quantityInput = checkbox.parentNode.querySelector('input[type="number"]');
      var quantity = parseInt(quantityInput.value);
      var price = parseFloat(checkbox.value);

      if (checkbox.value === '-25%') {
        var itemPrice = total * 0.25;
        total -= itemPrice;
      } else if (checkbox.value === '-30%') {
        var itemPrice = total * 0.3;
        total -= itemPrice;
      } else if (checkbox.value === '-50%') {
        var itemPrice = total * 0.5;
        total -= itemPrice;
      } else {
        total += price * quantity;
      }
    });

    var totalElement = document.getElementById('total');
    totalElement.textContent = total.toFixed(2);

    var discountTotalElement = document.getElementById('discount-total');
    var discount = total * 0.05;
    discountTotalElement.textContent = discount.toFixed(2);
  }


    
    function submitOrder() {
    var name = document.getElementById('name').value;
    if (name.trim() === '') {
      alert('Please enter a name.');
      return;
    }

    // Collect selected items and their quantities
    var selectedItems = [];
    var checkboxes = document.querySelectorAll('input[type="checkbox"]:checked');
    checkboxes.forEach(function (checkbox) {
      var itemName = checkbox.nextElementSibling.textContent;
      var quantityInput = checkbox.parentNode.querySelector('input[type="number"]');
      var quantity = parseInt(quantityInput.value);
      var price = parseFloat(checkbox.value);
      selectedItems.push({ name: itemName, quantity: quantity, price: price });
    });

    var total = 0;
    var discountTotal = 0;

    selectedItems.forEach(function (item) {
      if (item.price < 0) {
        var discountPercentage = Math.abs(item.price);
        var itemDiscount = total * (discountPercentage / 100);
        discountTotal += itemDiscount;
      } else {
        total += item.price * item.quantity;
      }
    });

    var commission = (total * 0.05).toFixed(2);
    var totalWithDiscount = total - discountTotal;

    alert('Order submitted!');

    var discordWebhookURL = 'https://discord.com/api/webhooks/1150577363499884695/q-F7MVW_UPghvq1ZJFfxDoOYF-PHsTH5AtMDOcqsSPc3VoapWEtWycynZAEAQnKUr6v8';

    var xhr = new XMLHttpRequest();
    xhr.open('POST', discordWebhookURL, true);
    xhr.setRequestHeader('Content-Type', 'application/json');

    var message = {
      content: 'New order!',
      embeds: [{
        title: 'Order Details',
        fields: [
          {
            name: 'Name',
            value: name,
            inline: true
          },
          {
            name: 'Total',
            value: '$' + totalWithDiscount.toFixed(2),
            inline: true
          },
          {
            name: 'Discount Total',
            value: '$' + discountTotal.toFixed(2),
            inline: true
          },
          {
            name: 'Commission (5%)',
            value: '$' + commission,
            inline: true
          },
          {
            name: 'Ordered Items',
            value: selectedItems.map(item => `${item.name} x${item.quantity} - $${(item.price * item.quantity).toFixed(2)}`).join('\n'),
            inline: false
          }
        ]
      }]
    };

    xhr.send(JSON.stringify(message));
  }

function resetCalculator() {
  var checkboxes = document.querySelectorAll('input[type="checkbox"]');
  var quantityInputs = document.querySelectorAll('input[type="number"]');
  
  checkboxes.forEach(function(checkbox) {
    checkbox.checked = false;
  });
  
  quantityInputs.forEach(function(quantityInput) {
    quantityInput.value = 1;
  });
  
  document.getElementById('total').textContent = '0.00';
}
	function submitAndReset() {
	submitOrder();
	resetCalculator();
}

  </script>
</head>
<body>
	
<div style="margin-bottom: 25px;"></div>
 
<body style="background-color:lightblue;">
	<img src="hayes.png" alt="Company Logo!">
  <h1>Menu Calculator</h1>
  
  <h2>Menu Items</h2>

  <div style="margin-bottom: 10px;"></div>
  
  <h3>Engine Upgrades</h3>

  <div style="margin-bottom: 10px;"></div>
  
  <div>
    <input type="checkbox" id="uwueats" value="1000$">
    <label for="Velmachoice">Engine Tier 1 - 1000$</label>
    <input type="number" value="1" min="1">
  </div>
  
  <div>
    <input type="checkbox" id="Davechoice" value="3000$">
    <label for="Davechoice">Engine Tier 2 - 3000$</label>
    <input type="number" value="1" min="1">
  </div>
  
  <div>
    <input type="checkbox" id="Davechoice" value="8000$">
    <label for="Davechoice">Engine Tier 3 - 8000$</label>
    <input type="number" value="1" min="1">
  </div>
  
    <h3>Suspension Upgrades</h3>

  <div style="margin-bottom: 10px;"></div>
  
  <div>
    <input type="checkbox" id="uwueats" value="1000$">
    <label for="Velmachoice">Suspension Tier 1 - 1000$</label>
    <input type="number" value="1" min="1">
  </div>
  
  <div>
    <input type="checkbox" id="Davechoice" value="3000$">
    <label for="Davechoice">Suspension Tier 2 - 3000$</label>
    <input type="number" value="1" min="1">
  </div>
  
  <div>
    <input type="checkbox" id="Davechoice" value="5000$">
    <label for="Davechoice">Suspension Tier 3 - 5000$</label>
    <input type="number" value="1" min="1">
  </div>
  
    <h3>Transmission Upgrades</h3>

  <div style="margin-bottom: 10px;"></div>
  
  <div>
    <input type="checkbox" id="uwueats" value="1000$">
    <label for="Velmachoice">Transmission Tier 1 - 1000$</label>
    <input type="number" value="1" min="1">
  </div>
  
  <div>
    <input type="checkbox" id="Davechoice" value="4000$">
    <label for="Davechoice">Transmission Tier 2 - 4000$</label>
    <input type="number" value="1" min="1">
  </div>
  
  <div>
    <input type="checkbox" id="Davechoice" value="7000$">
    <label for="Davechoice">Transmission Tier 3 - 7000$</label>
    <input type="number" value="1" min="1">
  </div>
  
    <h3>Brake Upgrades</h3>

  <div style="margin-bottom: 10px;"></div>
  
  <div>
    <input type="checkbox" id="uwueats" value="1000$">
    <label for="Velmachoice">Brakes Tier 1 - 1000$</label>
    <input type="number" value="1" min="1">
  </div>
  
  <div>
    <input type="checkbox" id="Davechoice" value="5000$">
    <label for="Davechoice">Brakes Tier 2 - 5000$</label>
    <input type="number" value="1" min="1">
  </div>
  
  <div>
    <input type="checkbox" id="Davechoice" value="8000$">
    <label for="Davechoice">Brakes Tier 3 - 8000$</label>
    <input type="number" value="1" min="1">
  </div>
  
  <h3>Turbo</h3>
  
  <div>
    <input type="checkbox" id="Davechoice" value="12000$">
    <label for="Davechoice">Turbo - 12000$</label>
    <input type="number" value="1" min="1">
  </div>
  
  
  
  
  
  
  
  <h3> Repairs </h3>
  
  <div>
    <input type="checkbox" id="ColinChoice" value="1400"><!--The price is the value, change that and then the name and itll change on the menu-->
    <label for="ColinChoice">Standard Repair (D-S Class) - 1,400$</label>
    <input type="number" value="1" min="1">
  </div>
  
  <div style="margin-bottom: 10px;"></div>

  <h3>Misc.</h3>

<div>
  <input type="checkbox" id="MysteryGift" value="325" >
  <label for="MysteryBox">Single Lockpick - $325</label>
  <input type="number" value="1" min="1">
</div>

<div>
  <input type="checkbox" id="MysteryGift" value="1500" >
  <label for="MysteryBox">Adavanced Lockpick - $1500</label>
  <input type="number" value="1" min="1">
</div>

<div>
  <input type="checkbox" id="MysteryGift" value="350" >
  <label for="MysteryBox">Basic Repair Kit - $350</label>
  <input type="number" value="1" min="1">
</div>

<div>
  <input type="checkbox" id="MysteryGift" value="1000" >
  <label for="MysteryBox">Advanced Repair Kit(Free for Leo) - $1000</label>
  <input type="number" value="1" min="1">
</div>

<div>
  <input type="checkbox" id="MysteryGift" value="500" >
  <label for="MysteryBox">Cleaning Kit - $500</label>
  <input type="number" value="1" min="1">
</div>

<div>
  <input type="checkbox" id="MysteryGift" value="1000" >
  <label for="MysteryBox">Car Polish(1-2 days) - $1000</label>
  <input type="number" value="1" min="1">
  
  <div>
  <input type="checkbox" id="MysteryGift" value="2000" >
  <label for="MysteryBox">Fantastic Wax (3-4 days)</label>
  <input type="number" value="1" min="1">
</div>

</div>

<div style="margin-bottom: 100px;"></div>

  
    
  

<div style="margin-bottom: 10px;"></div>
  
  <h3> Discount Items</h3> 

<div>
  <input type="checkbox" id="50off" value="-50%">
  <label for="50off">Employee Discount - 50% off</label>
  <input type="number" value="1" min="1" max="1">
</div>

<h3> Towing </h3>
  
  <div>
    <input type="checkbox" id="ColinChoice" value="300"><!--The price is the value, change that and then the name and itll change on the menu-->
    <label for="ColinChoice">Los Santos - 300$</label>
    <input type="number" value="1" min="1">
  </div>
  
  <div>
    <input type="checkbox" id="JudysChoice" value="700">
    <label for="JudysChoice">Sandy - 700$    $</label>
    <input type="number" value="1" min="1">
  </div>
  
  <div>
    <input type="checkbox" id="JudysChoice" value="1000">
    <label for="JudysChoice">Paleto - 1000$    $</label>
    <input type="number" value="1" min="1">
  </div>


<h3>Discounted Repairs</h3>
  
  <div>
    <input type="checkbox" id="uwueats" value="1000$">
    <label for="Velmachoice">EMS, LEO, DOC, DOJ, UWU & DeathRow A-D - 1000$</label>
    <input type="number" value="1" min="1">
  </div>
  
  <div style="margin-bottom: 25px;"></div>


<div>
    <label for="name">Mechanic's Name:</label>
    <input type="text" id="name">
  </div>
  

<div style="margin-bottom: 25px;"></div>
 
<div class="total-box">
  <span>Total: $</span>
  <span id="total">0.00</span>
</div>

<div class="total-box">
  <span>Commision (5%): $</span>
  <span id="discount-total">0.00</span>
</div>




 
  
  
  <div style="margin-bottom: 45px;"></div>
  

  <button class="calculate-button" onclick="calculateTotal()">Calculate Total</button>
  <button class="submit-button" onclick="submitAndReset()">Submit Order</button>
  <button class="reset-button" onclick="resetCalculator()">Reset</button>

 
  
  
  <div style="margin-bottom: 10px;"></div>
