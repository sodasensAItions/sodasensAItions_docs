# **Requirement Analysis**

# **Functional Requirements**

* **AI-driven drinks ordering**  
  * The app will make use of a form of Artificial Intelligence that will receive the list of ingredients available and, making use of this list, form automatically a drink for the user to order.  
  * The AI should prefer ingredients that the user rated higher and neglect those the user rated lower.  
* **Registering and Login**  
  * The user will be able to create an account and login using it. Data about the customer such as first name, last name, email, and saved drinks will be stored.  
  * Users will be able to save drinks to their account, allowing for fast ordering the next time they wish to purchase a drink.  
* **Paying for order**  
  * The app will make use of the Stripe payment system in order to pay for drinks using the secure Stripe API.  
  * This payment information will not be held in the database, instead the user will be able to sign into their Stripe account or enter their payment information.  
* **Creating your own drink**  
  * The user, on top of being able to automatically generate a drink through AI, should be able to craft a drink of their own choosing. The customer will be presented with a list of all possible ingredients and be able to add whichever they choose.  
* **Location-based drinks creation**  
  * The user will be able to opt into a service which makes use of the GPS tracking on their phone. When the user nears the building (exact distance yet to be defined), a notification will be sent to the shop they have ordered to, notifying the robot that it should begin the drinks preparation so that it will be ready on arrival of the user.  
  * If the user decides to opt out of this service, the user will instead be presented with a button that, when pressed by the user, informs the robot that they are close, initiating the drinks preparation.  
* **Rating your drink**  
  * The user should be able, after obtaining their drink, to be able to rate their drink on a Likert scale of 1-5, with 5  being the most positive, and 1 being the least.  
  * These ratings given to drinks must affect future recommendations given by the AI, whether that be to recommend a certain type of ingredient more, or to use a certain ingredient less.  
* **Drinks are to be stored in a cooled box until the customer's arrival**  
  * After purchasing a drink and after its creation, the drink will be placed into a secure cool box for pick up by the customer. The customer will be required to enter a code presented to them on their app in order to unlock their specified cool box and retrieve their drink.

# **Nonfunctional Requirements**

## Non-Functional Requirements for the Customer App:

**Performance**

* The app should load within 3 seconds to ensure a smooth user experience.  
* It should provide smooth scrolling and minimal delays during interactions, such as when users navigate through the app.  
* The response time for any action, such as adding items to the cart or checking out, should not exceed 1 second.

**Scalability**

* The app must be designed to handle a growing number of users, especially during busy periods.  
* It should also support the addition of new features without requiring significant changes to the architecture.

**Usability**

* The app must be easy to navigate, providing a user-friendly interface that caters to both regular and new users.  
* It should offer accessibility options, such as larger font sizes or voice commands, to accommodate users with varying needs in later versions.  
* Supporting multiple languages is essential to ensure it is accessible to a diverse customer base. This should be included in later versions, while the first version will only be available in English.

**Availability**

* The app must be available on the Android platform. An iOS app should be implemented as soon as possible.  
* A high level of uptime is crucial, with a target of 99.9% uptime to minimize disruptions and ensure continuous availability to users.

**Security**

Customer data, especially sensitive information such as payment details, must be encrypted to ensure privacy and security.

* Multi-factor authentication should be implemented to secure user accounts and prevent unauthorized access.  
* Regular security audits are necessary to identify vulnerabilities and ensure the app remains secure.

**Compatibility**

* The app should run smoothly on various screen sizes and device models, ensuring that it works consistently across different devices.  
* It should also be compatible with older operating system versions, allowing users with older devices to access the app without issues.

**Maintainability**

* The app's codebase should be designed in a modular way to allow for easy updates and bug fixes.  
* Automated testing should be implemented to ensure that new features do not interfere with or break existing functionalities.

**Accessibility**

* The app must be WCAG compatible so that it is accessible to all users.

---

## Non-Functional Requirements for the Server:

**Performance**

* The server should be able to handle at least 1,000 concurrent orders per second during peak times to meet high demand.  
* API response times should be below 300 milliseconds for standard requests to ensure a fast and responsive system.

**Scalability**

* The server's architecture should support horizontal scaling, meaning it can handle an increasing number of users by adding more resources, such as load balancers.  
* It should be able to dynamically scale up or down based on traffic surges, especially during special events or promotions.

**Availability**

* The server should have an uptime of 99.99%, with robust failover systems in place to handle any unexpected outages.  
* Regular backups and disaster recovery measures should be implemented to prevent data loss in case of a server failure.

**Security**

* Passwords must be encrypted both in transit and in the database to protect sensitive information.  
* The server must comply with industry standards when handling payment data.  
* Regular security patches and continuous monitoring should be implemented to detect and mitigate potential threats.

**Maintainability**

* The server architecture should be modular, allowing for easier updates and modifications without disrupting service.

**Monitoring and Logging**

* Comprehensive logging must be implemented to track user activities, server performance, and order transactions for future analysis and troubleshooting.  
* Real-time monitoring tools should be in place to detect issues with server load, latency, or failures, allowing for prompt response to any problems.

**Latency**

* The system should be designed to ensure low latency for real-time order updates and status tracking, providing users with a seamless experience.

**Compliance**

* The server must comply with data protection regulations, such as GDPR, if the business serves customers in regions with strict data privacy laws.  
* Proper management of user consent should be implemented for data collection and usage, ensuring compliance with legal requirements.

---

# **Business Requirements**

## **Admin Server**

A dedicated server is provided for business administrators and maintenance technicians to access tools for metrics analysis, maintenance, and future planning.

### **Revenue**

The system tracks revenue based on incoming customer payments and outgoing costs such as inventory replacement, API costs, and other relevant financial metrics.

* *Revenue Calculation*: Revenue is calculated as incoming payments minus outgoing costs.  
  * *Outgoing costs*: Includes inventory replacement and API costs.

  #### **Analytics**

    #### Basic profit and cost breakdown with the ability to analyze revenue over various periods.

  * *Visual Representation*: Use pie charts and bar graphs for clarity.  
  * *Analysis Range*: Options include month-to-month, year-to-year, and specific date ranges.

  #### **Customer Transactions**

    Transaction records are kept for payment amounts and the ingredients used per transaction to track inventory depletion.

  #### **Inventory Replacement**

    #### The system manages and monitors both soft and hard inventory. AI is responsible for anticipating and restocking inventory before it runs out.

  * *Soft Items*: Includes soda fountain syrup, fruit juices, etc.  
  * *Hard Items*: Cups, lids, straws, drink carriers, etc.

  ### **Maintenance**

    ### The system handles maintenance through work orders and emergency malfunction notifications.

  * *Work Orders*: Automatically generated for repair needs.  
  * *Emergency Handling*: Notifies technicians and temporarily halts operations if critical malfunctions occur.

  ### **Security and Access Controls**

    ### Ensures that only authorized personnel have access to sensitive business data and analytics in the admin server.

  * *Role-Based Access*: Different levels of access control for business administrators, maintenance staff, and external contractors.  
  * *Data Encryption*: Sensitive customer and business information is encrypted both in storage and during transmission.

  ### **User Engagement Metrics**

    ### Metrics to monitor user interactions, including customer activity and session durations.

  * *Active Customer Count*: Displays the number of customers actively interacting with the soda shop AI at any given time.  
  * *Session Duration*: Tracks the average session length per user, helping identify customer engagement trends.  
  * *Retention Rates*: Tracks how often customers return to place orders, providing insight into overall satisfaction and engagement.

  ### **AI Performance Analysis**

    ### Tracks the effectiveness and impact of the AI's interactions with customers.

  * *Success Rates*: Measures how often AI-powered features such as drink customization or recommendations lead to completed orders.  
  * *Sentiment Analysis*: Analyzes customer feedback and interactions with AI to measure overall satisfaction and detect areas for improvement.  
  * *Common Requests*: Identifies popular drink combinations and frequently asked questions to improve future AI responses.

  ### **Data Export and Reporting**

    ### Provides tools to export analytics and financial data for further reporting and analysis.

  * *Data Formats*: Exports in multiple formats (CSV, Excel, etc.) for use in external analytics tools.  
  * *Report Generation*: Automated report creation for business insights, financial summaries, and performance metrics.  
  * *Scheduled Reports*: Allows users to schedule periodic data exports, enabling regular monitoring of key metrics.

---

# 

# **User Requirements**

**Sign-In/Sign-Up:**

* Users can create an account or log in using an email and password.  
* Users will remain signed in after their first login, with an option to sign out.

**Drink Ordering:**

* **Quick Order**: Users can quickly place a drink order using:  
  * AI-generated suggestions based on preferences.  
  * Customization options for creating a personalized drink.  
  * Selecting saved favorite drinks.  
  * Choosing from the daily menu.

**Order Management:**

* Users can view the drinks in their current order.  
* Ability to add multiple drinks to a single order.  
* Option to edit or delete drinks within an order before confirming.

**Order History & Reordering:**

* Users can view their past order history.  
* One-click reordering of previously purchased drinks.

**Payments:**

* Secure payment options for completing drink orders directly through the app.

**Store Notifications:**

* Notify the store when they are nearby, allowing for quicker drink preparation.  
* Receive a notification when their drink is ready for pickup, with instructions on which box or counter to collect it from.

**Ratings and Reviews:**

* Users can rate and review drinks after their purchase, providing feedback for future improvements.

**MoSCoW**  
---

**Must-Have**

* The app must have an android app implementation (IOS and web implementations are discussed below)  
* The user must be able to create an order of one or more drinks through the app. The drink ordering system will allow the user to   
  * Select a drink from a premade menu  
  * Select a drink from the user’s order history  
  * Create a custom drink using a combination of any of the available ingredients  
    * A reasonable limit will be set for how many ingredients can be added  
  * Have the app’s AI create a custom drink, using a combination of available ingredients  
* The user should be able to review drinks already added to the order, make changes to those drinks, or delete them  
* The user must be able to pay from within the app using a credit / debit card  
* The user must be able to notify the store when the arrive through the app  
* After an order has been picked up, the app must allow the user to rate their drink on a scale of 1-5. Ratings will be used for custom drink preferences.   
* The app must notify the user when their drink is available  
* There must be a simple server, demonstrating the app’s capabilities to communicate with the robot.  
  * The server must display a message when a drink order arrives \- including the components of the drink  
  * This server can be used by the engineering team to connect the app to the robot  
* Admin must be able to view basic analysis and statistic data stored on the server


---

**Should-Have**

* The store should have an inventory system, notifying the app when an ingredient is out so it can no longer be ordered from the app.   
  * Why: This functionality, will be very important to avoid issues that could occur if a user tries to order a drink that’s out of stock \- but a working demo of the app could still be built assuming everything stays in stock  
* The user should be able to select from several different store locations \- gps can be used to determine the nearest one.   
  * Why: Having an app that functions completely for one location is better than having one that doesn’t function at all. Once a working demo of the app has been built, we can expand to multiple locations  
* In addition to notifying the user when their drink is ready, the exact pickup box will also be shown.   
  * Why: Knowing where their drink is located would be beneficial to the user, but the user could still manage to find their drink without this feature.  
* Admin should be able to view maintenance information through the admin server. There should be security and access controls to protect customer data.  
  * Why: This feature is not essential to the core MVP, but will immensely help as the product enters the maintenance phase.  
    

---

**Could-Have**

* The app could notify the server when the device is approaching the store, so drinks can be prepared in advance  
  * Why: Because a user will have to opt in to using location data, an alternative will have to be put in place regardless. This feature could take some time to implement, therefore, our priority will be in building this alternative, then expanding to location-based usage if there is time.  
* The app could have a built in rewards program for ordering drinks  
  * Why: This feature could be helpful in advertising efforts for the company, but isn’t essential at all to the app functionality, Our priority will be to implement essential features before expanding to extras.   
* The app could be ported to web and IOS devices  
  * Why: Eventually, it would be important for this app to be accessible from multiple different devices. Once a functional app is built, creating ports will take significantly less time than the original. That being said, we would like to build a working demo, even if only on one platform, rather than having a partial app on every platform.   
* Filters could be available for AI drink recommendation, filtering out unwanted ingredients or allergies  
  * Why: This is another feature that will for sure be added to future versions of the app, but isn’t essential to the core functionality. For now a user with allergies can manually remove flavors they can’t have from an AI generated drink.   
* Admin could have additional analytic views in the admin servers, including AI performance analysis, user engagement metrics, and an option to export analytic data.  
  * Why: These features could improve the user experience in the long run, but will have no initial benefits for the user. Not a should have like maintenance because that will immediately benefit the user once the product is shipped.  
    

---

**Won’t-Have**

* The app won’t have a custom chatbot for customer support  
  * Why: This is a feature that can be considered for future visions of the app, but would take a significant amount of time and money to incorporate. Spending development time on this feature would distract from the core functionality of the app.  
* The app won’t link to social media for sharing drinks in this iteration  
  * Why: This is another feature that can be considered for future versions of the app, but would distract development efforts and isn’t essential to the core functionality of the app. 

**Use Case Stories**  
---

**Customer Use Case Stories:**

* **As a customer, I want to create an order by selecting a premade drink, a previous order, or customizing one** with a set number of available ingredients, ensuring my drink fits within predefined limits for ingredient combinations.  
* **As a customer, I want the app’s AI to suggest personalized drink options** by analyzing my order history and combining available ingredients, providing me with unique, tailored recommendations.  
* **As a customer, I want to be able to rate the AI suggested drinks,** which can be used to further improve suggestions in the future.  
* **As a customer, I want to review my selected drinks before finalizing the order**, so I can adjust ingredients, quantities, or remove drinks to make sure everything is correct before proceeding to payment.  
* **As a customer, I want to pay securely within the app using my credit or debit card,** so I can complete my transaction without needing to handle payments in-store, making the process smooth and safe.  
* **As a customer, I want to receive a notification when my drink is ready for pickup,** ensuring that I’m informed the moment my drink is prepared, reducing wait time.  
* **As a customer, I want to notify the store when I arrive** for pickup with a single tap in the app, so the staff knows I’m there and can prepare my drink for quick handoff.  
* **As a customer, I want to rate my drink after picking it up,** offering a 1-5 rating along with optional comments, so the app’s AI can better understand my preferences for future orders.  
* **As a customer, I want the app to clearly indicate which pickup box my drink is stored in,** so I can retrieve it efficiently without confusion.  
  ---


#### **Admin Use Case Stories:**

* **As an admin, I want to manage the menu in real-time,** ensuring that ingredients and drinks reflect accurate availability by updating or removing them instantly as stock changes.  
* **As an admin, I want instant notifications when new orders are placed**, showing the exact details of the drinks ordered and customer preferences, so I can manage fulfillment efficiently.  
* **As an admin, I want the app to automatically disable out-of-stock ingredients,** preventing customers from selecting unavailable items, reducing order errors and customer dissatisfaction.  
* **As an admin, I want to track customer feedback and ratings across all stores,** so I can adjust the menu and inventory based on real-time preferences and trends.  
* **As an admin, I want to manage multiple store locations via a centralized dashboard,** assigning orders to the appropriate store based on the customer’s location for faster service.  
* **As an admin, I want to access detailed reports on order trends, ingredient usage, and revenue performance,** so I can make informed decisions about inventory management and store operations.  
  ---


#### **Maintenance Use Case Stories:**

* **As a maintenance worker, I want to monitor the robot’s connectivity with the app server**, ensuring that orders are processed smoothly and communicated accurately between systems.  
* **As a maintenance worker, I want to receive immediate alerts for server or robot malfunctions**, so I can troubleshoot issues and resolve them before they impact the customer experience.  
* **As a maintenance worker, I want to perform diagnostic checks on the server-robot connection**, identifying and preventing potential issues before they cause disruptions.  
* **As a maintenance worker, I want to remotely restart or troubleshoot the robot**, allowing me to quickly address issues without needing to be on-site, minimizing downtime.

**Use Case Diagram**

Customer Diagram

Admin Diagram