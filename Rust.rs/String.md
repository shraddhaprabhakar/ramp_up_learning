The data in borrowed string slice cannoyt be modified whereas the data is String can be modified.
A borrowed string slice is a subset of the String in more than 1 way.
Both have valid UTF-8
We cannot access strings using index as there are so many languages out there including emogies which all add up to unicode and string is a unicode so that becomes complex.
A borrowed string slice is internally made up of a pointer to some bytes and a length.
A string is made up of a pointer to some bytes, a length and capacity that may be higher than what is being used.
You can use string.bytes() to access the string index bytes or .char() method but technically its very complex.
