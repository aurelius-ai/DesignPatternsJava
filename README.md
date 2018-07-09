#### Completed:
       Downloaded Professor's templates and instructions ... 
       Deleted all files from repository ... 
       Watched all vidoes and lectures posted as of 7/9/2018 4am CST ...  
       Installed and experimented with Maven ... 
       Installed Git and GitDesktop Software ... 
       Rough Diagrams created ... 
       Listing assumptions ...

### Assumptions:
##### 1.) Tasked with creating a hot beverage machine that offers at least three types of espresso, three types of tea and two condiments, I am including additional options of regular coffee and decaf, because otherwise the machine would be adding condiments to espresso drinks and tea, which most often are served with no condiments.
##### 2.) This machine is providing free beverages and therefore must be accessed by an exclusive group in a private space, such as Boston University's campus. The first menu option will ask if the user is a student or faculty member of Boston University, and if not will deny the user access, returning to the main menu.
##### 3.) The program's output messages are to be displayed on a drink machine and this may be a small screen displaying only capital letters. For this reason, the messages in the console are succinctly worded in capital letters.
##### 4.) Milk and Sugar are not behaviors when being chosen as options in the user menu, but adding steamed milk, foamed milk, sugar, cinnamon, chocolate or extra water is a behavior in the context of brew behavior as there are specific amounts designated that cannot be altered without changing the name of the espresso drink.  Therefore the addition of espresso condiments is not accomplished as part of the user menu but instead by EspressoBrewBehaviorStrategy.  Additions of Milk and Sugar to Coffee and tea are otherwise satisfied like a decorator pattern, wrapping condiments.
##### 5.) A beverage machine would only have buttons for available entries (integers), it should therefore not be necessary to catch exceptions for entry types that would be impossible for a the machine with such limited buttons.  Instead, entries not within the scope of the menu will restart the program at the first menu.
##### 6.) Delicate and Dark Teas are steeped at different tempuratures for different lengths of time, as are Espressos Drinks and Regular Coffee, necessitating a timerBehaviorStrategy (with four time groups of 0.5, 3, 4 and 5) and a heatBehaviorStrategy (with four tempurature groups of 165, 180, 195 and 205).


### Abstract GrandParent Class: MenuOption
      // to easily pass instances between methods, especially during menu item selection
      Abstract Parent Class of all Teas, EspressoDrinks, Coffees, and Condiments
### Parent Abstract Class: Condiment
#### MilkChoice Decorator Classes: SoyMilkDecorator, SkimMilkDecorator, and CreamDecorator
#### Sweetener Decorator Classes: SteviaDecorator, SplendaDecorator and SugarDecorator

## Context Objects
   #### Abstract Classes: Tea, Coffee, EspressoDrink
       Tea is parent of all tea varieties
       Coffee is parent of Regular and Decaf
       EspressoDrink is parent of all espresso varieties

## TimerBehaviorStrategy and HeatBehaviorStrategy (double minutes and int heat)
       // Behavior Strategies for all Espresso, Teas, and Coffees
       // additional behavior strategy EspressoBrewBehaviorStrategy makes possible avariety of EspressoDrinks
#### Recommended steep times and tempuratures for various teas, espresso drinks and coffee are listed below:
       https://www.artoftea.com/recommended-steep-times
       https://www.thespruceeats.com/how-to-brew-tea-water-temperatures-766316
       https://blackbearcoffee.com/resources/87
       https://www.ncausa.org/About-Coffee/How-to-Brew-Coffee
       http://justcoffee.coop/how-to-pull-a-perfect-espresso-shot/
       https://www.1stincoffee.com/art-of-making-espresso
#### Teas with equal values are grouped by an abstract class (below):
### abstract class QuickTea
       // teas that share quickTime and teaHeat behaviors
       GreenTea: 3 minutes at 180º F
       DarjeelingTea: 3 minutes at 180º F
### abstract class DelicateTea
       // teas that share teaTime and lowHeat behaviors
       JasmineTea: 4 minutes at 165º F
       YellowTea: 4 minutes at 165º F
       WhiteTea: 4 minutes at 165º F
### abstract class DarkTea
       // teas that share teaTime and espressoHeat behaviors
       BlackTea: 4 minutes at 195º F
       OolongTea: 4 minutes at 195º F
### abstract class Coffee
       // drinks that share coffeeTime and coffeeHeat behaviors
       Reg and Decaf Coffee: 5 minutes at 205º F
### interface InterHeatBehaviorStrategy 
       // 4 subclasses:
       lowHeat = 165 // for Jasmine and White Tea
       teaHeat = 180 // for Yellow, Green and Darjeeling Tea
       coffeeHeat = 205 // for Regular and Decaf coffee
       espressoHeat = 195 // for all espresso drinks and oolong and black tea 
       /** espressoHeat is shared by black, oolong, and all espresso drinks */
### interface InterTimeBehaviorStrategy
       // 4 sublcasses:
       quickTime = 3 // for Green and Darjeeling Tea
       teaTime = 4 // for all Delicate Teas and Dark Teas
       coffeeTime = 5 // for Decaf and Regular Coffee
       espressoTime = 0.5 // 30 seconds for all espresso drinks
### interface EspressoBrewBehaviorStrategy ... String espressoBrewBehavior; 
       addEspresso // print "adding shot of espresso" (all espresso drinks, twice for DoubleEspresso)
       addSteamedMilk // print "steamed milk added" (Cappuccino, and LatteMachiatto - child of Latte)
       addFoamedMilk // print "foamed milk added" (LatteMachiatto - variant of Latte)
       addChocolate // prints "chocolate added" (Mocha Latte and Cinnamon Mocha Latte - variant of Latte)
       addCinnamon  // prints "cinnamon added" (Cinnamon Dolce Latte and Cinnamon Mocha Latte - variants of Latte)
       addWater // prints "water added" (Americano)
### abstract grandparent class EspressoDrink
       // drinks that share espressoTime and espressoHeat behaviors
       All Espresso Drinks: 0.5 minutes at 195º F
       /** The brew time for espresso is 30 seconds
         * Espresso brew temperature is the same for black and oolong tea
         * Espresso shares its heatBehaviorStrategy with black and oolong tea
         */
 ### Espresso 
       // parent class of Americano and DoubleEspresso and abstract Latte
       addEspresso() // EspressoBrewBehaviorStrategy
 #### DoubleEspresso 
       // (aka doppio) inherits EspressoBrewBehaviorStrategy from Espresso adds shot of espresso
       addEspresso() twice 
 #### Americano
       //  inherits EspressoBrewBehaviorStrategy from Espresso, adds water
       addWater() and addEspresso()
 #### abstract class Latte 
       /* 
        * Actual lattes contain more milk than a cappuccino but for optimal use of class inheritance:
        * The abstract parent class Latte has only minimum/cappucino quantities of steamed and foamed milk.
        * Cappucinos contain 1/3 steamed milk, 1/3 espresso and 1/3 foamed milk. 
        * Cappuccino inherits this EspressoBrewBehaviorStrategy without change from the abstract class Latte.
        * All subclasses of Latte contain steamed milk and foamed milk but vary by proportions
        * (and some contain chocolate and/or cinnamon).
        */
   ##### Cappuccino 
       //inherits EspressoBrewBehaviorStrategy from Latte, adds nothing
       addSteamedMilk(), addEspresso(), addFoamedMilk()
   ##### Cinnamon Mocha Latte
       // inherits EspressoBrewBehaviorStrategy from Latte, adds chocolate and cinnamon 
       addSteamedMilk(), addEspresso(), addFoamedMilk(), addChocolate(), addCinnamon()
   ##### Cinnamon Dolce Latte
       // inherits EspressoBrewBehaviorStrategy from Latte, adds cinnamon
       addSteamedMilk(), addEspresso(), addFoamedMilk() addCinnamon() 
   ##### Latte Macchiatto
       // inherits EspressoBrewBehaviorStrategy from Latte, adds extra steamed milk
       addSteamedMilk() twice, addEspresso(), addFoamedMilk() 
   ##### Mocha Latte 
       // inherits EspressoBrewBehaviorStrategy from Latte, adds chocolate
       addSteamedMilk(), addEspresso(), addFoamedMilk(), addChocolate()

### Other Classes
      ConsoleOutput 
      Main Class (contains main method)
      Caution (to warn user that beverage is hot and alerts end of program cycle)

