class KioskSystem {
  constructor() {
    this.sellers = { admin: "password123" };
    this.categories = {
      Pasta: {},
      Desserts: {},
      Drinks: {},
    };
    this.cart = {};
  }

  authenticateSeller() {
    const username = prompt("Enter Username:");
    const password = prompt("Enter Password:");
    if (this.sellers[username] === password) {
      alert("Authentication successful.");
      return true;
    }
    alert("Authentication failed. Try again.");
    return false;
  }

  sellerMenu() {
    while (true) {
      const choice = prompt("SELLER MENU: LOGOUT, ADD, REMOVE").toUpperCase();
      if (choice === "LOGOUT") {
        alert("Logged out.");
        break;
      } else if (choice === "ADD") {
        this.addItem();
      } else if (choice === "REMOVE") {
        this.removeItem();
      } else {
        alert("Invalid choice. Try again.");
      }
    }
  }

  addItem() {
    const category = prompt(
      "Choose a category to ADD an item: Pasta, Desserts, Drinks"
    );
    if (!this.categories[category]) {
      alert("Invalid category. Try again.");
      return;
    }

    while (true) {
      const itemName = prompt("Enter the name of the item to add:");
      const itemPrice = parseFloat(
        prompt("Enter the price of the item:")
      ).toFixed(2);

      this.categories[category][itemName] = parseFloat(itemPrice);
      alert(`${itemName} added to ${category} with price $${itemPrice}.`);

      const continueAdding = prompt("Continue to ADD? (yes/no)").toLowerCase();
      if (continueAdding !== "yes") break;
    }
  }

  removeItem() {
    const category = prompt(
      "Choose a category to REMOVE an item: Pasta, Desserts, Drinks"
    );
    if (!this.categories[category]) {
      alert("Invalid category. Try again.");
      return;
    }

    while (true) {
      const itemName = prompt("Enter the name of the item to remove:");
      if (this.categories[category][itemName]) {
        delete this.categories[category][itemName];
        alert(`${itemName} removed from ${category}.`);
      } else {
        alert("Item not found in category.");
      }

      const continueRemoving = prompt(
        "Continue to REMOVE? (yes/no)"
      ).toLowerCase();
      if (continueRemoving !== "yes") break;
    }
  }

  customerMenu() {
    while (true) {
      const choice = prompt("CUSTOMER MENU: ORDER, CART, CANCEL").toUpperCase();
      if (choice === "ORDER") {
        this.placeOrder();
      } else if (choice === "CART") {
        this.manageCart();
      } else if (choice === "CANCEL") {
        alert("Exiting customer menu.");
        break;
      } else {
        alert("Invalid choice. Try again.");
      }
    }
  }

  placeOrder() {
    const category = prompt(
      "Choose a category to ORDER from: Pasta, Desserts, Drinks"
    );
    if (!this.categories[category]) {
      alert("Invalid category. Try again.");
      return;
    }

    const itemName = prompt(
      `Available items in ${category}: ${Object.keys(this.categories[category]).join(
        ", "
      )}\nEnter the name of the item to order:`
    );
    if (!this.categories[category][itemName]) {
      alert("Item not found in category.");
      return;
    }

    const quantity = parseInt(
      prompt(`Enter the quantity of ${itemName}:`),
      10
    );
    if (isNaN(quantity) || quantity <= 0) {
      alert("Invalid quantity. Try again.");
      return;
    }

    if (!this.cart[itemName]) {
      this.cart[itemName] = {
        price: this.categories[category][itemName],
        quantity: 0,
      };
    }
    this.cart[itemName].quantity += quantity;

    alert(
      `${quantity} ${itemName}(s) added to cart. Total: $${(
        this.cart[itemName].price * this.cart[itemName].quantity
      ).toFixed(2)}`
    );
  }

  manageCart() {
    while (true) {
      const choice = prompt("CART MENU: PRINT, ADD, REMOVE, CANCEL").toUpperCase();
      if (choice === "PRINT") {
        this.printCart();
      } else if (choice === "ADD") {
        this.placeOrder();
      } else if (choice === "REMOVE") {
        this.removeFromCart();
      } else if (choice === "CANCEL") {
        alert("Exiting cart menu.");
        break;
      } else {
        alert("Invalid choice. Try again.");
      }
    }
  }

  removeFromCart() {
    const itemName = prompt(
      `Items in cart: ${Object.keys(this.cart).join(", ")}\nEnter the name of the item to remove:`
    );
    if (this.cart[itemName]) {
      delete this.cart[itemName];
      alert(`${itemName} removed from cart.`);
    } else {
      alert("Item not found in cart.");
    }
  }

  printCart() {
    if (Object.keys(this.cart).length === 0) {
      alert("Cart is empty.");
      return;
    }

    let totalPrice = 0;
    const cartDetails = Object.entries(this.cart)
      .map(([itemName, { price, quantity }]) => {
        const itemTotal = price * quantity;
        totalPrice += itemTotal;
        return `${itemName}: $${price.toFixed(
          2
        )} x ${quantity} = $${itemTotal.toFixed(2)}`;
      })
      .join("\n");

    alert(`CART:\n${cartDetails}\n\nTotal Price: $${totalPrice.toFixed(2)}`);
  }

  start() {
    while (true) {
      const userType = prompt("Are you a SELLER or CUSTOMER?").toUpperCase();
      if (userType === "SELLER") {
        if (this.authenticateSeller()) {
          this.sellerMenu();
        }
      } else if (userType === "CUSTOMER") {
        this.customerMenu();
      } else {
        alert("Invalid input. Try again.");
      }
    }
  }
}

// Initialize the kiosk system
const kiosk = new KioskSystem();
kiosk.start();
