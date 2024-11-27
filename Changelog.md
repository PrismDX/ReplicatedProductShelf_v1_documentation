# ReplicatedProductShelf Changelog

### v1.15 - *27. Nov 2024*
- Added product crate max capacity to product info ( MaxCrateCapacity )
- Added Product crate icon to product info ( ProductIcon )
- Added new variable to product crate ( bUseProductIcon ) to toggle product icon
- Added the option to not reset slot if its empty 
- Added new variable to product slot ( bResetEmptyShelf )
- Added new function to product slot ( GetProductCount - Returns product count and instanced static mesh count ) 
- Removed unnecessary code from RemoveShelf function (Product slot)
---
### v1.1 - *12. Nov 2024*
- Moved pricetag to BP_Productslot to avoid any issues and extra setup for price tags when used as a child actor component. limited to 1 price tag for now. See BP_ProductSlot -> Variables for pricetag configuration
---