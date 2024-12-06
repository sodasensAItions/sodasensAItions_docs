This sprint the Tylers worked on finding a replacement to the failed AI from last sprint. We experimented with a VAE architictur, a procedural regressive model. The VAE barely did better than the GANS from 
last sprint, but we did have surprising success from the procedural model. This sprint we were able to assemble sufficient training data for the model, and fully train the procuderal data. We wrote an API
to communicate between applicatoin and the model file (hosted in the app) and created a basic page to display AI generated drinks. The generate drink page wasn't hooked up to be able to able to add new drinks 
to the order this sprint. 

We also worked on implementing the Edit drinks page. We were not able to fully complete this page by the end of the sprint, as there were still some issues with UI elements, and dropdowns not scrolling. These
issues should be easily resolvable next sprint. 

We added a payment system using the Stripe library. Using stripe was somewhat difficult, and took many hours of work. At this point there were still some issues with the payment system, so this task was pushed 
back to the next sprint. We were able to fully implement the basket to track drinks that have been added to an order. 

Finally some work was done on planning and implementing the sign in, sign up, and sign out endpoints. We were able to implement the sign in page and get that working. 

For the most part we were able to accomplish most of our tasks this sprint. There were a few bugs with some of our features, but we put enough work in that resolving them next sprint shouldn't take too long.  


