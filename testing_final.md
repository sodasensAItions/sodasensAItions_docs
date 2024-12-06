# AI (model creation and training)

Because it is impossible (and not necessarily desirable) to train the AI to be perfect, we couldn’t take a traditional approach to unit testing. Instead, we used 85% of our training data in the training process of the AI. Using the built in functionality of the Tensorflow model, we were able to use the remaining 15% of the training data to evaluate the model.

The AI model would rate each possible output on a scale of 0 to 1 indicating how likely it is to be correct. Our goal with training was to have a mean absolute error of 0.1 \- meaning that the model’s actual output was, on average 0.1 off from the expected output. Our model was able to achieve a mean absolute error of 0.08. 

We also followed the automatic testing of our model by manually checking some of the AI generated drinks. We were wanted to observe if the model followed some of the following guildles (obtained from patterns we observed in the training dataset)

* A drink shouldn’t have more than 5 total squirts  
* A drink shouldn’t have more than 3 squirts of a single flavor \- and only up to two for heavier flavors like cinnamon and cream .  
* A drink shouldn’t have only one squirt of flavor, unless it is a heavier flavor

The automatic testing of the accuracy of the model helped guide our decision making in adjusting training parameters to the model. There weren’t any major design flaws with the final model’s code, but some slight adjustments to the model helped improve accuracy. 

Our manual system testing on the  model revealed surprisingly good results. We expected a few exceptions to the above rules due to the imperfect nature of the AI, but were surprised to find no noticeable exceptions. 

# Front-End

Unit testing in Android comes in two flavors: local and instrumented. The design principles of Android is to separate the business logic from the UI components. Doing so allows for the core logic of the app to be tested without relying on Android resources (it can be performed on any computer as opposed to an emulator). The instrumented testing can be used to perform actions in the actual app. 

While Android’s instrumented test framework seems really powerful we were unaware of its existence until the end of the testing sprint. As a result, we located as much code as possible to the business portion of the app to reduce the likely-hood of a bug in the UI layer. We also designed steps to manually test the integration of UI and business logic \- walking through each test with the final version of our app. 

Because we were not aware of the UI testing framework, our UI architecture was not designed to be compatible with the testing framework. In order to make our UI code Unit testable, we would have to refactor most navigation elements \- which would not be feasible in the remaining time. For this sprint, we will stick to our plan of manually testing UI elements. 

The first below section covers our unit-tested business logic. The next section covers the steps to run though the manual system testing.

## Unit Testing

As stated before, our unit tests cover the business logic of the app. We estimate that \>90%  of our business logic is being unit tested. The unit testing is divided into the following areas. We actually didn’t discover any new bugs via unit testing, but it was helpful to prevent regressions after updates to the code base. 

Probably one of the more weakly tested parts of our code was the cart integration. The cart of drink orders was too closely tied to the Android components to be individually unit tested, and would require too much refactoring to be able to do in this sprint. 

### AI API

Most of the testing on the AI was done before exporting the model to the app (see AI section). We didn’t want to hard-code specific expected values into the unit test, as these could change if improvements were made to the model. The goal of unit testing in the android app was to make sure that the model was actually returning values, that the values were in the correct format, and that the returned values were reasonable (the AI should give some sort of recommendation for a drink with no flavor, and should stop giving recommendations for drinks with lots of flavors).

### Drink Recommendation Page

The drink recommendation page was responsible for using the AI API to procedurally create new drink flavors. We wanted to test that this class was capable of creating a list of unique drinks, and would always generate a new drink when requested unless no new unique drinks could be generated. We also tested the refresh functionality of the recommendations page.   
If we were to perform the test’s with our AI model, we would be severely restricted on what we could test due to the unpredictable nature of the AI model. Therefore we chose to use a mock AI to be able to fully test this class’s ability to use the API. Mochito, a mocking library for Java and Kotlin, was helpful in doing this. 

One of the most difficult parts of testing this page was dealing with multiple asynchronous coroutines. To help the UI seem smooth, the drink generation was done on a background thread \- and could take an unknown amount of time to complete. We were able to deal with this by using a feature of the Kotlin testing framework that allowed for manual coroutine management \- allowing for us to wait for all coroutines to finish before testing the result of an operation. 

### Drink Creation Page

Most of the unit testing in this section was easy. We simply wanted to make sure that calling functions to update the state of the drink actually resulted in a change of state in the drink class. This page also integrated the AI to provide ingredient recommendations. We tested to make sure that the AI recommendations were updated as the drink was modified. Again the AI was mocked in this test to provide predictable results. 

### Sign in / Sign Up Page

We chose to mock the server in writing this test to ensure that the test can complete without needing a running server. The code to directly access the server was also closely tied to Android components, and would have been impossible to separate for the sake of unit testing. 

The goal of testing this component was to ensure that the state was correctly updated when the UI calls functions in the sign in business logic; make sure that local data validation worked correctly; make sure that the state correctly updated when getting a success or error response from the server. 

## System Testing

The goal of the system testing was to test the overall integration of different parts of the app, and test UI components that could not easily be testable. We followed the below processes with our final version of the app to ensure that it was working correctly before deployment. As described above, it would have been helpful to automate these tests, but doing so wouldn’t be possible in this sprint. 

As a note, many of the tests involve rotating the screen. Correct Android design states that data (such as fields being edited by the user) should not be stored on the UI layer because information can be lost when a refresh is triggered. There are many events that can trigger a refresh, such as changing to and from dark theme, getting a phone call, and navigating away from the app. Rotating the screen is one of the easiest ways to trigger a refresh in testing. 

1. Navigate to the Drink Generation page (*label 1.1*) and perform the following tests:   
   1. Scroll through the generated drinks from each page, and ensure that drinks are generated in a reasonable amount of time. Scrolling back to previously viewed drinks should not change those drinks.   
   2. Pull down on the screen, to refresh drinks. The lists should be replaced with new lists of drinks, in a reasonable amount of time.   
   3. Rotate the screen triggering a refresh, while it is acceptable for the scroll position to change, the contents of each list should still be in the same order.   
   4. Select a drink from the list, this should navigate to the edit drinks page, filled with the drink’s information. Ensure that all information is filled correctly, and save the drink.   
   5. Repeat the above step with a different AI generated drink. Navigate to the cart and ensure that both drinks have been correctly added, with no information changed.   
2.    
   1. Add a drink from the menu (*label 1.3)* and navigate to the cart, observing that the drink has been correctly added  
   2. Select “edit” and make sure that all relevant drink information has been correctly filled out.   
   3. Edit the name, ingredient list, base and ice quantity. Rotate the screen to trigger a refresh and ensure that all information remains changed.   
   4. Save the drink and edit the same drink again to make sure that all changed fields remain changed.   
   5. Repeat the same steps with a drink originating from the Generate Drinks (*label 1.1)* page, and my drinks page (*label 1.2)*.   
3.    
   1. Add two identical drinks from the menu and navigate to the cart, make sure that two identical entries have been added.   
   2. Select “edit” on one drink, change some fields, and save.   
   3. Navigate back to the drink menu and ensure that only one copy of the drink has been modified.   
   4. Repeat the above steps with two identical drinks originating from the AI and user drinks pages.   
4.    
   1. Navigate to the “my drinks” page and press the button to create a new drink. Change all fields, and rotate the screen to ensure that no information has been lost  
   2. Save the drink, and make sure that it has been added to the cart  
   3. Edit the drink and make new changes, ensure that the changes are also reflected.   
5.    
   1. Restart the server, ensuring that no user information is being stored.   
   2. Enter a user name and password, an error should be shown at the bottom of the sign-in screen, and the user shouldn’t be signed in  
   3. Navigate to the create account screen, leave the alternate leaving each field blank and attempt to sign in; whenever there is an empty field, an appropriate error should be displayed.   
   4. Retry, entering valid values for each field. The app should automatically navigate back to the sign in screen.   
   5. Enter the correct username, but incorrect password for the sign-in screen; an error should be displayed.   
   6. Enter an incorrect username, but correct password for the sign-in screen; an error should be displayed.   
   7. Enter the correct username and password, the app should navigate to the home screen.   
6.    
   1. Sign in using valid credentials \- the app should navigate to the home menu  
   2. Close the app and reopen, the user should automatically be signed in   
   3. Test placing and paying for an order \- these require a valid token and would fail if the user hasn’t been properly signed in. It is expected that they should succeed following the above steps  
7.    
   1. Enter a few drinks into the basket  
   2. Navigate over to the basket and select the payment button  
   3. A payment dialog should pop up \- enter Stripe’s valid sign in information   
      1. Card number:  4242 4242 4242 4242\.  
      2. Any cvv number can be used  
      3. Any valid expiration date can be used  
      4. Any valid zip code can be used  
   4. Using valid payment, a payment success message should be shown  
   5. Add some new drinks again, navigate to the basket and attempt to pay with an invalid (declined card)  
      1. Card number:  4000 0000 0000 9995  
      2. Any cvv number can be used  
      3. Any valid expiration date can be used  
      4. Any valid zip code can be used  
   6. A message should appear saying the card has insufficient funds

From following the above system tests, we were able to find quite a few bugs in the app. 

First off, our apps state wasn’t being stored correctly, so triggering a refresh caused data to be lost in the sign in screen, sign up screen, and edit drink screen. We also found that different drinks in the basket referred to the same drink or ingredient list in code \- meaning that if one was edited the others would be too. Interestingly, we also found a bug in Stripe’s payment library, entering a month on the expiration date that didn’t begin in 0 or 1 would crash the app (for example entering 4 instead of 04 for the month would crash the entire app). This bug was fixed in a newer version of Stripe. 

# Back-End

Unit testing for the server is described below. System testing was done in conjunction with the front-end, and is described in the Front-End section of this document. 

## Unit Testing

In this project, unit testing is implemented using the JUnit framework, which is a popular testing framework for Java. The tests are designed to verify the functionality of the various components of the application, such as controllers, services, and repositories

Our backend unit tests run HTTP requests against our endpoints in a running server and then assert the expected results. Our unit tests cover 100% of our endpoints. Not only did we write test cases that test endpoints with valid input, we also focused on data that the server should reject. Writing unit tests with the Java Spring framework using JUnit is really easy, so we didn’t run into any really difficult pieces of our app to test, though we did run in to a little “feature” of gradle that causes it to run tests that are in a test suite as both part of a test suite and an individual test. This caused us a little bit of a headache for a while, but when we figured it out we just deleted our test suite organization and ran all tests individually. Due to testing we can be reasonably sure that our implementation is correct.

In this project, each test case can be executed separately using the JUnit framework. Here is a general description of how each test case is executed, how data is created for each test case, and how it is queried from the database to confirm the changes:

1. **Test Case Execution**  
   1. Each test case is annotated with \`@Test\`, which tells JUnit to execute the method as a test.  
   2. You can run individual test cases or the entire test class using your IDE (IntelliJ IDEA) or a build tool like Gradle.  
2. **Data creation**  
   1. **Setup**: Before each test case, necessary data is set up. This can be done in a method annotated with @BeforeEach, which runs before each test method.  
   2. **Test Data:** Test data is created within the test method itself. For example, creating an Account, SodaOrder, or Drink object and saving it to the database.  
3. **Database interaction**  
   1. **Saving Data**: Data is saved to the database using repository methods. For example, accountRepository.save(account) saves an Account object to the database.  
   2. **Querying Data**: After performing actions in the test, data is queried from the database to verify the changes. This is done using repository methods like findById or custom query methods.  
   3. **Assertions**: The queried data is then compared with the expected results using assertions. For example, `Assert.assertEquals(expected, actual)` checks if the actual data matches the expected data.  
4. **Teardown**  
   1. **Cleanup**: After each test case, any necessary cleanup is performed. This can be done in a method annotated with @AfterEach, which runs after each test method. This ensures that each test case runs in isolation without affecting others.