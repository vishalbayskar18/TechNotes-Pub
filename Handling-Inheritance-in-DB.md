Suppose you support different types of pen in your system e.g. Gel Pen, Ball Pen, Fountain Pen.

Then you create 1 base table (parent table) e.g. in this case pen and add all the common attributes in the pen table.

And you will have specific tables (child tables) which will have specific attributes only.

E.g. in pen you will store, ID, Name, Price

and in Gel Pen Table you will store, ID and InkType, ID for reference in the parent table and InkType because it’s specific to Gel Pen.

In case you don’t follow this and take approach where you will have only 1 table for all the type of Pen, then there will be lots of fields which will be empty.

Or if you have different tables for different type of pen then lots of data would be duplicated.
