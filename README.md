# ReplicatedProductShelf_v1_documentation


# Contents

**4 Blueprints**
- Actor component
- Shelf slot
- Product crate
- Price tag

**2 Enumerators**
- Notification
- Product type
	
**1 Structure**
- Product info

*+ additional example content used in the showcase map*

---


# Setup:
 
**#1.** Add BP_ProductCharacterComponent to your player character by opening your character blueprint and click add in the components tab and then search for BP_ProductCharacterComponent and then click it to add it to your character. This should now appear in your components window and let you change the variables within it.

# 
**#2.** Make sure your character has replication enabled in the details panel and double check that the BP_ProductCharacterComponent has "Component Replicates" enabled ( Should be by default ).
#

 **#3.** Adjust the interaction distance in the details panel in BP_ProductCharacterComponent that has been added to the character to make sure the interaction line trace reaches where you want depending on your camera setup (e.g. Firstperson or Thirdperson). You'll be able to see the line trace if you have Debug enabled.

#
 
 **#4.** I recommend to turn on debug mode in the product character component if its not enabled already for some feedback and aiming until you integrate your notification UI and to see if the inputs are actually working.


---

# How it works

This works by picking up a product crate ( *BP_ProductCrate* ) using the character component added to your player character ( *BP_ProductCharacterComponent* ). When you are carrying a product crate, you will be able to interact with the product shelves ( *BP_ProductSlot* ) by adding and removing products to it.

Product crates are currently attached to the camera with a relative transform for demonstration purposes and is done in *BP_ProductCharacterComponent->AttachCrate* function and dropped by using *BP_ProductCharacterComponent->DetatchCrate* if you want to change it or change the position of it.


----


# Default Inputs
	
- [ WASD ] - Move

- [ Mouse movement ] - Look around

- [ Left mouse button ] - Add product to shelf

- [ Right mouse button ] - Remove product from shelf

- [ F ] - Grab product crate

- [ G ] - Drop product crate

***Inputs can be changed at Blueprints/Components/BP_ProductCharacterComponent -> input graph.***

---

# Showcase map

This includes some examples on how you can use the blueprints and recommended mesh requirements in order for it to work properly.

This map uses an example character which is essentially just a First person character template with removed mesh and gun and added BP_ProductCharacterComponent.
	

---

# Blueprints


### BP_ProductCharacterComponent

This component handles most of the interaction replication and inputs such as Pick up/drop product crate and add/remove from shelf.

UI Notifications can be setup in the On_Notify function in this component located here: BP_ProductCharacterComponent -> FUNCTIONS -> Product Component -> Actions -> On_Notify  assuming you have UI/Widget for notfications.

#
**Variables:**

- **Enable Debug (bool)**: 

	This enables debug mode which will alow you to see error messages using print string and draw the line trace used.

- **Interaction Distance (float)**:

	This is used to determine how long the line trace will be ( how far you can interact with the blueprints ).

---
### BP_ProductCrate

This blueprint is the product crate that the player is holding which contains product info and product count. This is used to put products in the product shelf aswell as remove them and add it to the product crate.

#
**Variables:**

- **ProductCount (Integer)**:
 
	This determines how many products inside the product crate.
- **Product (Product Struct)**: 

	This contains the information from the Product info structure ( *Struct_ProductInfo* )

---
### BP_PriceTag

This blueprint is an actor which contains a text component used to display the price of the product in shelf ( currently takes price from the product crate )

---
### BP_ProductSlot

This blueprint is a shelf slot and is meant to be used multiple times. (Actor tick is disabled by default and gets enabled when needed (Interpolation)).

It uses instanced static mesh so it can support alot of "products" in the shelf also allowing to have many shelves active without unnecessary drawcalls.
	
I recommend that you create a blueprint that will act as a shelf (static mesh) with 1 or more product slots ( and price tags if you want that )	

Max product count in the shelf slot is calculated by the product mesh size (mesh bounds) + the active spacing between products you use, so bigger products = less space and smaller = more.

Simply just scale the actor for more space and it will update accordingly

Products added to a shelf is also assigned random rotation depending on the Rotation range ( *Product Info* ) to make it more inconsistent with product placement.

#
**Variables:**

- **ProductType (Product Type Enum)**:

	This determines what the allowed product type for the shelf ( *Enum_ProductTypes* ) and is used to see if the product crate product has the same type when adding or removing products from the shelf.

- **bEnableDebug (bool)**: 	

	This enables debug mode which will alow you to see the surface area and bounds used to calculate shelf size as well as debug messages using print string. Instanced static mesh position is also indicated by the white arrow.
	
- **Price Tags (Array *BP_PriceTag* reference)**: 
	
	This allows you add and select multiple *BP_PriceTag* blueprints from the world using the picker tool to connect it to the product shelf so the product shelf can update the text value in *BP_PriceTag* when the first product is added to the shelf.

- **Spring Effect (bool)**: 

	Interpolate product centering instead of instantly placing it at centered position ( determined by mesh size, max count ( determined by mesh size and surface area ) and spacing ) adding a spring like effect to the products when it centers the instanced static mesh.

- **Spring Speed (float)**:
	
	This determines how fast the interpolation happens if SpringEffect(bool) is enabled.

- **Use spacing from product (bool)**:

	When enabled, this will use the spacing value that is in the product info of the product you are adding to the shelf. This spacing value will be added between the products in the shelf.

- **Shelf product spacing (Vector2D)**:

	This is the spacing value for X and Y when placing products. This only works when *use spacing from product* is disabled
	



---


# Product Info Structure
Product info for the products.
#
**Variables:**

- **Mesh (Static mesh)**: 

	This is the static mesh used for the product when placed in shelf.

- **Price (float)**: 
	
	This is the price that will be displayed if using price tag. 

- **Product type (Product Type Enum)**: 

	This is the product type used to match the product shelf when placing / removing products

- **Name (Text)**: 
	
	Product name, used for shelf conditions and product crate label.

- **bStackable (bool)**: 
	
	This determines if the product can be stacked on the Z Axis.

- **Rotation Range (Vector2D)**:

	Random rotation range for products when they are in shelf. X = min rotation, Y Max rotation.

- **ZMultiply (float)**:
	
	This is used to fine tune if pivot point is at the center of product on the Z Axis.

- **Product Spacing (Vector2D)**:
	
	This is used in shelf if UseProductSpacing is enabled on the shelf slot.

---
