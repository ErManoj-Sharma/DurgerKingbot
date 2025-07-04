
## Project Description:

# 🚀 BurgerKing Bot Clone – Built with Next.js

A fast and responsive Burger King chatbot web clone built using Next.js. This project replicates a real-world food ordering experience via Telegram-style bot interaction, enabling users to browse menus, place orders, and make payments seamlessly.

### 🔹 Key Features:

#### 🧠 Interactive chat-based UI inspired by Burger King's ordering bot
#### ⚡ Built with Next.js for server-side rendering and SEO benefits
#### 💳 Payment integration with Razorpay/Stripe (custom amount & callbacks)
#### 🍔 Dynamic menu with emojis, quantity handling, and total price calculation
#### 🔐 User session management with Redux Toolkit
#### 🌐 Telegram Web App support with bot-to-app communication
#### 📱 Mobile-first, responsive design
#### 🔍 Tech Stack: Next.js, React, Redux Toolkit, Tailwind CSS, Razorpay API, Telegram Bot API

## 🌟 Star This Repo

If you found this project useful, please consider giving it a ⭐️ to show your support and help others discover it!

[![GitHub Stars](https://img.shields.io/github/stars/ErManoj-Sharma/DurgerKingbot?style=social)](https://github.com/ErManoj-Sharma/DurgerKingbot)

---

## 📦 Clone & Run Locally

```bash
# 1. Clone the repo
git clone https://github.com/ErManoj-Sharma/DurgerKingbot
cd DurgerKingbot

# 2. Install dependencies
npm install

# 3. Add your environment variables
cp .env.example .env.local
# Fill in values for Telegram bot token, Razorpay/Stripe keys, etc.

# 4. Run the development server
npm run dev
```
## Bot setup
1. go to @botfather in telegram 
2. give command `/mybots`.
3. select your desired bot or if you dont have any bot then create a new bot by command `/newbot`.
4. after selecting bot click on `bot setting` option.
5. click on `menu button`
6. pass url of your web app.
7. give title to menu button.
8. again back to bot settings and click on `configure mini app`.
9. click on `enable mini app` and give url to it 
10. if you don't have url right now then don't worry , while running dev server use ngrok to get and `https` url and pass url to here.
11. each time you stop ngrok and restart it , ngrok will genrate new url so repeat step 5-9 when you stop ngrok server

# configuration
```javascript
// put this script in head of next app inside rootlayout.js
<script src="https://telegram.org/js/telegram-web-app.js"></script>
``` 

# .env.local
```python
# at root of project create .env.local 
RAZORPAY_KEY="XXXXXXXXXXXXXX"
RAZORPAY_SECRET="XXXXXXXXXXXXXXX"
TELEGRAM_BOT_TOKEN="XXXXXXXXXXX"
```
# Api calls
Next doesn't allow to call api directly by frontend
so use this way 
1. make a dir `src/pages/api/<apiService.js>`
2. here a make a api handler 
3. make a serivce to call api at `src/services/<Apicallservice>.js` 
4. if you are using redux for state management then you can invoke this service in Slice as well to store api response in store
5. whenever you add any new api endpoint, `restart` the server else it doesn't run properly

# redux toolkit 
next doen't allow directly to wrap html dom 
so use this way
1. create a `ProviderWrapper`
   ```js
   "use client";
   
   import { Provider } from "react-redux";
   import { store } from "@/Store/Store";
   
   export default function ProviderWrapper({ children }) {
     return <Provider store={store}>{children}</Provider>;
   }
   ```
2. now wrap dom in this wrapper
   ```js
   export default function RootLayout({ children }) {
     return (
       <html lang="en">
         <head>
           <script src="https://telegram.org/js/telegram-web-app.js"></script>
         </head>
         <body className={`${geistSans.variable} ${geistMono.variable} antialiased`}>
           <ProviderWrapper>
             {children}
           </ProviderWrapper>
         </body>
       </html>
     );
   }
   ```
# Callbak Issue
if you use payment gateway then it will redirect to callback url 
, at callback url data of localstorage, sessionstorage and redux store is wiped up. 

so pass the necessary and reqiured info in callback url as searchparams and at callback url page use api to retrive data