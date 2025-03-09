# Movie Bucks

**Movie Stock Market Game Overview**

This Movie Stock Market Game is a fun and engaging simulation where users can buy, sell, and trade movie tickets (stocks) based on the success of movies in the real world. The prices of these movie stocks fluctuate just like stocks in a traditional stock market, and users make decisions based on predictions, trends, and available data.

## Key Features:

**Movie Bucks (MB)**: In-game currency used for buying and selling movie stocks.

**Dynamic Stock Prices**: Prices fluctuate based on the performance of movies (box office earnings, reviews, etc.).

**Buy/Sell Mechanism:** Users trade stocks with each other, and their trades influence stock prices.

**Real-World Data Integration:** Stock prices are based on real-world metrics like box office earnings, social media trends, and audience reviews.

## Money Flow & Currency System

In-Game Currency (**Movie Bucks**) are the primary currency within the game. They are used to buy and sell movie stocks. Each user gets a set amount of Movie Bucks at the start (e.g., 1000 MB).

**Daily/Weekly Bonuses**: Players earn Movie Bucks for logging in, completing tasks, or achieving milestones.

**Stock Performance**: If a user buys a stock and the movie performs well in the market, they make a profit when selling.

**Purchasing Movie Bucks:**

**In-App Purchases (IAP):**

Users can purchase Movie Bucks using real money. (Example: $1 = 100 MB, $5 = 500 MB, etc.)

**Subscription Packages:**

Players can subscribe to a monthly plan to get a regular supply of Movie Bucks, along with other benefits like reduced trading fees or access to exclusive movie stocks.

### **Buying and Selling Movie Stocks**

**Market Fluctuation:**

The price of each movie stock is influenced by both real-world data (box office earnings, reviews, social media buzz) and user behavior (buying/selling actions).

**Buying Stocks:**

Users spend Movie Bucks to buy stocks of movies they believe will perform well.
Users can buy as many stocks as they want, provided they have enough Movie Bucks.

**Selling Stocks:**

Users can sell their movie stocks for Movie Bucks based on the current stock price.
If the stock price increases after they buy, they earn Movie Bucks by selling at a higher price. Conversely, if the price falls, they incur a loss.

**Market Dynamics:**

Supply and Demand: If many users buy the stock of a particular movie, the price goes up. If they sell, the price goes down.
Transaction Fees: A small fee is deducted when buying and selling stocks. This helps maintain the balance of the in-game economy.

## Monetization Strategy

The game will generate revenue primarily through in-app purchases, advertisements, and premium memberships.

### Revenue Generation Methods:

**In-App Purchases (IAP):**

Users can purchase Movie Bucks to progress faster in the game, access premium stocks, or gain advantages in trading.

**Ad Revenue:**
*Interstitial Ads:* Show ads after trades or major game events to earn Movie Bucks.
*Rewarded Video Ads:* Users can watch videos for Movie Bucks.

**Subscription Model:**
VIP memberships give access to exclusive features such as reduced transaction fees, extra Movie Bucks, exclusive movie stocks, and more.

**In-Game Store:**
Users can purchase non-intrusive cosmetic items (e.g., profile customization) or power-ups (e.g., "Stock Analyzer" tool to predict market movements).

## **Technical Design Considerations**

The **Movie Bucks Game** leverages a combination of **Serverpod**, **Flutter**, and **multiple APIs** to build a dynamic, scalable, and cost-effective system. The system is designed to reduce unnecessary API calls, maximize performance, and efficiently handle real-time data for an engaging user experience.

---

### **Core System Components**

To ensure the game is robust, scalable, and cost-effective, the following core components are key to the design:

#### **1. Movie Bucks Engine**

This is the heart of the system that manages:

- **Stock Price Calculation**: Uses a combination of:
  - **Real-world data** (Box office earnings, ratings, and social media sentiment).
  - **In-game behavior** (User buy/sell actions to simulate supply and demand).
- **Price Volatility Logic**: Movie Bucks will follow a weighted formula combining:
  - Box office performance (e.g., opening weekend earnings, sustained revenue flow).
  - User trading volume (more trades = greater volatility).
  - Sentiment analysis from social media platforms for buzz-driven fluctuations.
- **User Influence on Market**: Each buy/sell action will trigger a price recalculation, ensuring user behavior has a meaningful impact.

#### **2. APIs Integration**

We will integrate multiple APIs to ensure diverse and accurate data points. These APIs may include:

- **Box Office API**: For revenue data (e.g., Box Office Mojo, The Numbers).
- **Movie Rating APIs**: For aggregating scores from IMDb, Rotten Tomatoes, and Metacritic.
- **Social Media APIs**: For measuring movie buzz via Twitter, Reddit, etc.

By integrating multiple APIs, we ensure **data redundancy** — reducing the risk of downtime and incomplete data. If one API fails, alternative sources can fill the gaps.

#### **3. Game Logic Engine**

Responsible for:

- Implementing game-specific rules that determine how stock values respond to user behavior and real-world events.
- Managing time-based changes (e.g., price resets every 24 hours for volatility control).
- Calculating bonuses, streaks, and user milestones to encourage engagement.

#### **4. Movie Vault System**

- Each movie "stock" will have an associated **Vault Item** that acts as a unique asset tied to that film.
- Vault Items will evolve with the movie's timeline — starting as a "New Release," progressing to "Cult Classic" or "Old Favorite."
- Vault Items can be traded in bulk or split into smaller units for strategic trading.

#### **5. Transaction Fee Logic**

To simulate a real market and maintain balance:

- Every trade will incur a **transaction fee** (e.g., 1-3% of the total transaction value).
- This fee will be redistributed into the game’s **reward pool** to fund leaderboards, achievements, and special events.

---

### **Backend Architecture Using Serverpod**

We are heavily leveraging **Serverpod** for our backend to manage:

- **User Data & Authentication**: Serverpod will securely handle user profiles, transaction histories, and portfolios.
- **Game State Management**: The game engine logic will reside in Serverpod, ensuring price fluctuations, stock value adjustments, and data updates occur efficiently.
- **In-App Purchases (IAP)**: Transactions for buying **Movie Bucks** will be processed via Serverpod.
- **Caching & Data Efficiency**: To minimize API costs and improve performance, Serverpod's **built-in caching** will store frequently accessed data (e.g., movie performance metrics, stock prices) directly in the database.

#### **Cost-Efficiency Strategy Using Serverpod**

- Since movie data is often **static** (e.g., box office results only change daily), we'll cache data in Serverpod's database and refresh it on a timed schedule.
- Cached data will reduce API calls, cutting costs significantly while improving latency for end users.
- User portfolio values will be **locally calculated** via cached stock values rather than frequent API requests.

---

### **Monorepo Structure Using Melos**

To ensure scalability, modularity, and efficient collaboration, we will use **Melos** to manage the monorepo setup. The structure is as follows:

```
movie-bucks/
├── apps/
│   ├── movie-bucks-app/             # Main Flutter app for users (Game UI)
│   ├── movie-bucks-dashboard/       # Admin Dashboard for managing game rules, features, and user invites
│   └── movie-bucks-tweaks/          # Dev app for tweaking in-game rules and performing feature flags
│
├── packages/
│   ├── movie-bucks-engine/          # Core engine logic for movie stock pricing and market behavior
│   ├── movie-bucks-apis/            # Integrations with external APIs for real-time movie data
│   ├── movie-bucks-data/            # Data models, structures, and logic for movie stock data
│   ├── movie-bucks-transactions/    # Handles transaction logic, including fees, buying, and selling
│   └── shared-utils/                # Shared utility functions and helpers
│
├── melos.yaml                       # Configuration for Melos to manage multi-package monorepo
└── pubspec.yaml                     # Main configuration for the Flutter app
```

### **Key Monorepo Design Principles**

- **Separation of Concerns**: Each major feature is modular, ensuring scalability and easier testing.
- **Shared Logic**: Core logic (e.g., stock calculation, data models) will be developed in **packages** to reduce code duplication.
- **Admin App**: The `movie-bucks-dashboard` app will serve as a developer tool to tweak market rules, set feature flags, and invite testers.

---

### **Data Flow in the System**

1. **Data Retrieval**: APIs fetch fresh movie data on a timed schedule (e.g., every hour or day).
2. **Caching Layer**: Fetched data is stored in Serverpod’s **database cache** to reduce costs.
3. **Market Engine Logic**: The engine recalculates prices based on:
   - Real-world data (API updates).
   - User actions (buy/sell behavior).
4. **User Actions**: Users trade stocks via the Flutter app, which updates Serverpod instantly.
5. **Serverpod Sync**: Updates are broadcast via **WebSockets** for real-time updates to all users.

---

### **Conclusion**

This enhanced design emphasizes:

✅ **Robust architecture** with modular code and scalable infrastructure.
✅ **Cost-effective data management** using **Serverpod caching** to reduce reliance on expensive API requests.
✅ **Dynamic gameplay mechanics** where user behavior directly affects the market.
✅ **Seamless real-time updates** via WebSockets to ensure users stay informed on market changes.

With this technical foundation, the Movie Bucks Game is positioned to deliver a fast, engaging, and strategic experience that blends entertainment with financial simulation.
