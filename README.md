# Herbal_Nutrition_project
The three parts of the file

The file has three layers:

HTML is the skeleton: the sections, buttons, forms and empty boxes such as #shopGrid and #cartBody.
CSS is the styling: colors, layout, the leaf animations and the dark and cream look.
JavaScript is the brain. It fills the empty boxes with products, handles clicks, and calculates prices.

To run it, you just double-click the file or upload it to any free host (GitHub Pages, Netlify). Nothing needs to be installed.

What happens when the page loads
The browser reads the HTML and shows the welcome screen, with its loading bar and rotating herb cards.
The JavaScript starts. It defines the product list (PRODUCTS) and the seed marketplace listings (SEED).
It then loads saved data from localStorage: the cart, wishlist, users and so on. If nothing is saved yet, it starts empty.
The last line runs paintAll(); renderCart(); renderWallet(); renderDash(); renderRev(); memory();. These functions turn the data into HTML and put it on the page.
When you click “Enter”, the welcome screen fades out and the shop is visible.
The core idea: data in, HTML out

Every render...() function follows the same pattern:

data (array of products)  →  build HTML text with .map()  →  put it into an element with innerHTML

For example, renderShop() filters PRODUCTS by the chosen category, builds a card for each with card(), and places the result in #shopGrid. When the data changes, the function runs again and the screen updates. The cart, wishlist and dashboard all work this way.

How clicks work

Buttons in the HTML carry a label like data-act="add" data-v="ash". That means “do the action add on product ash”.

One single listener on the whole page catches every click, reads data-act, and calls the matching function in the A object, so add calls A.add("ash"). This is why the file has so few separate event handlers.

Why data survives a refresh

The L.set() function saves data in localStorage, a small storage area built into every browser. Cart, wishlist, accounts, orders and reviews are saved there as text (JSON). When you reload, L.get() reads them back. This is also why:

Accounts and orders exist only on that one browser. If you open the site on another phone, they are not there.
Clearing browser data erases everything.
A typical customer journey
You browse the shop and click a category chip, which updates cat and calls renderShop().
You press Add, and the cart array gets the item. renderCart() recalculates the total with tot() and moves the free-shipping bar.
You play a mini-game and win a coupon (award()), which goes into your wallet.
At checkout you type the coupon, and applyCp() checks it against your wallet and reduces the price.
You submit the form, and the order is saved in cep-orders, the cart is cleared, and the “Thank You” animation plays.
How sellers and customers interact

A seller registers with the Seller role and adds a product, which is pushed into the market array and shown in the marketplace. A customer clicks “Contact”, which saves a message in cep-msgs. When the seller logs in on the same browser, the dashboard shows that message and they can reply. A real multi-user marketplace would need a server, because here both people share one browser’s storage.

The two “smart” parts
AI Herbalist: this is not real AI. It checks your sentence against keywords such as “sleep” or “stress” and returns a prepared answer with matching products.
Python section: the browser downloads a tool called Pyodide from the internet, which can run real Python code. The BMI plan and the savings finder are Python functions called from JavaScript. This part needs internet.
