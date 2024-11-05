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
Add BP_ProductCharacterComponent to your player character and you should be good to go 

I recommend to turn on debug mode in the product character component for some feedback and aiming until you integrate your notification UI and crosshair

Inputs can be changed at BP_ProductCharacterComponent -> input graph.

---


# Blueprints


### BP_ProductCharacterComponent

This component handles most of the interaction replication and inputs such as Pick up/drop product crate and add/remove from shelf.

	Variable Info soon

---
### BP_ProductCrate

This blueprint is the product crate that the player is holding which contains product info and product count. This is used to put products in the product shelf aswell as remove them and add it to the product crate.

	Variable Info soon

---
### BP_PriceTag

This blueprint is an actor which contains a text component used to display the price of the product in shelf ( currently takes price from the product crate)

	Variable Info soon

---
### BP_ProductSlot

This blueprint is a shelf slot and is meant to be used multiple times. (Actor tick is disabled by default and gets enabled when needed (Interpolation)).

It uses instanced static mesh so it can support alot of "products" in the shelf also allowing to have many shelves active without unnecessary drawcalls.
	
I recommend that you create a blueprint that will act as a shelf (static mesh) with 1 or more product slots ( and price tags if you want that )	

Max product count in the shelf slot is calculated by the product mesh size (mesh bounds) + the active spacing between products you use, so bigger products = less space and smaller = more.

Simply just scale the actor for more space and it will update accordingly

	Variable Info soon



---


# Replication

	information coming soon

---
