This assignment is to give you hands on experience writing a client and a server that communicate via XML messages transmitted via HTTP.  Technically this is not REST but you will see many people use this approach. (It is bad practice to design a web service this way)
Assignment Task

You are to read in the XML data file provided.  Then you are to allow the user to add 1 or more food items and retrieve 1 or more food items
AddFoodItem

URI	http://localhost:8080/FoodItems/webapi/inventory
HTTP Method	POST
Media Type	application/xml

Request Message

<NewFoodItems xmlns=”http://cse564.asu.edu/PoxAssignment”>
    <FoodItem country="GB">
        <name>Cornish Pasty</name>
        <description>Tender cubes of steak, potatoes and swede wrapped in flakey short crust pastry.  Seasoned with lots of pepper.  Served with mashed potatoes, peas and a side of gravy</description>
        <category>Dinner</category>
        <price>15.95</price>
    </FoodItem>
</NewFoodItems >


HTTP Response Codes 

Interpretation	Response Message
Food Item Added	<FoodItemAdded xmlns=”http://cse564.asu.edu/PoxAssignment”>
   <FoodItemId>156</FoodItemId>
</FoodItemAdded>

The FoodItemAdded is the Id your server generated for the new food item
Invalid or incorrect input message	<InvalidMessage xmlns=”http://cse564.asu.edu/PoxAssignment”/>

Food Item already in the Food List	<FoodItemExists xmlns=”http://cse564.asu.edu/PoxAssignment”>
   <FoodItemId>156</FoodItemId>
</FoodItemExists>

To test if the food item being added already exists in the list you test that the food item name and the category are the same
GetFoodItem

URI	http://localhost:8080/FoodItems/webapi/inventory
HTTP Method	POST
Media Type	application/xml

Request Message

<SelectedFoodItems xmlns=”http://cse564.asu.edu/PoxAssignment”>
   <FoodItemId>100</FoodItemId>
   <FoodItemId>156</FoodItemId>
</SelectedFoodItems>


HTTP Response Codes 

Interpretation	Response Message
All Food Item Retrieved	<RetrievedFoodItems xmlns=”http://cse564.asu.edu/PoxAssignment”>
    <FoodItem country="GB">
        <id>100</id>
        <name>Steak and Kidney Pie</name>
        <description>Tender cubes of steak, with tender lamb kidney is succulent rich gravy.  Served with a side of mashed potatoes and peas.</description>
        <category>Dinner</category>
        <price>15.95</price>
    </FoodItem>
    <FoodItem country="GB">
        <id>156</id>
        <name>Cornish Pasty</name>
        <description>Tender cubes of steak, potatoes and sweede wrapped in flakey short crust pastry.  Seasoned with lots of pepper.  Served with mashed potatoes, peas and a side of gravy</description>
        <category>Dinner</category>
        <price>15.95</price>
    </FoodItem>
</RetrievedFoodItems>
Food Item does not exist in the Food List	<RetrievedFoodItems xmlns=”http://cse564.asu.edu/PoxAssignment”>
    <FoodItem country="GB">
        <id>100</id>
        <name>Steak and Kidney Pie</name>
        <description>
           Tender cubes of steak, with tender lamb kidney is
           succulent rich gravy.  Served with a side of mashed
           potatoes and peas.
        </description>
        <category>Dinner</category>
        <price>15.95</price>
    </FoodItem>
    <InvalidFoodItem>
        <FoodItemId>156</FoodItemId>
    </InvalidFoodItem>
</RetrievedFoodItems>
Invalid or incorrect input message	<InvalidMessage xmlns=”http://cse564.asu.edu/PoxAssignment”/>
