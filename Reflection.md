Reflection:

Using the @property decorator makes my code cleaner and easier to read 
because I can access private attributes like regular variables — rect.width 
instead of rect.get_width(). Even though it looks like direct access, the 
getter and setter methods still run behind the scenes, so validation and 
encapsulation are maintained. For example, setting a negative width is 
automatically rejected by the setter. This gives me the safety of private 
attributes with the convenience of direct access, making my code more 
intuitive and easier to maintain.