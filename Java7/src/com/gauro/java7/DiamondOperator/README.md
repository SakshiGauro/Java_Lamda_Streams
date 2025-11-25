# Type Inference/Diamond Operator

Before Java 7, we have to create an object with Generic type on both side of the expression
like below:
Map<String, Integer> inputMap = new HashMap<String, Integer>();
• From Java 7, Java provides a improved compiler which is smart enough to infer the type of
generic instance. It simplifies the use of generics when creating an object.
• It is also called as Diamond operator. Using it we can create the object without mentioning
generic type on right side of expression like below:
Map<String, Integer> inputMap = new HashMap<>();
• Please note that we can’t use this diamond operator feature inside the anonymous inner class.
But this limitation is resolved in Java 9.


