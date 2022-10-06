---
aliases: [StringBuffer , StringBuilder ]
---

# StringBuffer
All Implemented Interfaces: *Serializable, Appendable, CharSequence*
-  **thread-safe, mutable** sequence of characters.
- has a **capacity**, it is automatically made larger.  capacity() return current
# StringBuilder
All Implemented Interfaces: Serializable, Appendable, CharSequence
- non-thread-safe but **faster** than StringBuffer (tell from the name, one foucus on building)
## Overall
The **StringBuilder** and **StringBuffer** class creates a **mutable** sequence of characters.   
Different than String, StringBuilder and StringBuffer are mutable. 

However the **StringBuilder** provides **no guarantee of synchronization** whereas the StringBuffer class does. And Regex, aka, regular expression, is used to match or filter out Strings.