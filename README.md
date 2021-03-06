This is a skeleton shopping basket implementation created in response to a code challenge. Here's the challenge...

_We must be able to:_

_Add items to the shopping basket_
_Remove items from the shopping basket_
_Empty the shopping basket_
_Additionally, we must be able to calculate the total value of the shopping basket accounting for:_

_Buy-one-get-one-free discounts on items_
_10% off on totals greater than £20 (after bogof)_
_2% off on total (after all other discounts) for customers with loyalty cards._
_We must be able to see the code running via passing tests or Terminal output._

_What we will be looking for:_
_Evidence of using a statically typed programming language and solid coding techniques with evidence of test driven development._

There are seven classes in my solution as follows:

1. **LoyaltyCard**: Supports the Discountable interface allowing it to calculate a revised total for the Customer.
2. **Customer**: May or may not have a loyalty card but supports the Discountable interface for use by ShoppingBasket.
3. **ProductOffer**: Calculates the price of a number of items of the same kind. Bogof and other types of offer can easily be supported.
4. **Product**: May or may not have an associated ProductOffer. Delegates calculation of price to ProductOffer if it exists.
5. **BasketDiscount**: Provided to ShoppingBasket at instantiation. May do nothing but it must exist. It is asked to discount the basket total when ShoppingBasket.getPrice() is called. 
6. **LineItem**: The ShoppingBasket comprises a number of LineItems. Each LineItem contains one Product and no two LineItems should contain the same Product. A LineItem wraps a Product up with a 'number of' and total price.
7. **ShoppingBasket**: A container for an array of LineItems with the methods required to manipulate them.

Points to note:
+ Its is assumed that some objects will originate from a database. Those objects have an 'id' field which is assumed to be unique amoungst the instances of the class (LineItem uses the Product id to identify different products).
+ All instances are duplicated as they are passed around. Thus the instances are isolated from changes that may be happening elsewhere in (what would probably be) a very large system.
+ Discounting mechanisms are assumed to change relatively frequently so have been separated out from the core classes using either the Strategy Pattern or Dependency Injection. This leaves the core classes open for extension but closed for change. The discount classes are LoyaltyCard, ProductOffer and BasketDiscount. The core classes are Customer (assumed to have address and credit card details in a real system), Product, LineItem and ShoppingBasket.