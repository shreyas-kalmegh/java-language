# Loggin Exceptions



When designing the logging of an application the question often arise: Where in the code should the exceptions be logged? Basically you have three different options:

1. Bottom Level Logging\
   Logging in the component where the exception occurs\

2. Mid Level Logging\
   Logging somewhere in the middle of the call stack, where sufficient information is available (the context of the component call)\

3. Top Level Logging\
   Logging centrally at the top of the call stack

### Top Level Logging

Logging at the top level means that you have a single, central place in the code that catches all thrown exceptions and logs them. In a Java web application that could be a control servlet or perhaps a servlet filter. In a desktop application perhaps you your event handlers would extend a base event handler capable of catching and logging all exceptions thrown.

The advantage of top level logging is that you only have a single spot in the application where logging code is written and maintained. In addition to being easier to implement, this also makes it easier to postpone the logging implementation until later in the development process if needed. The logging code will only have to be implemented in one place, and most likely won't change the total application call structure.

The disadvantage of top level logging is of course that this single central place doesn't know anything about what went wrong in the bottom level component that threw the exception, or what the mid level code calling that component was trying to do. That makes writing sensible log messages somewhat harder.

### Exception Enrichment

To overcome the lack of details available at the top level (and also to some degree at the mid level), you can enrich the exceptions as they propagate up the call stack towards the top level. Enriching exceptions is done by catching them, adding extra information and rethrowing them again. Rethrowing a caught Java exception will not change the embedded stack trace. The stack trace remains the same as when the exception was thrown first, by the bottom level component.

You will have to code your own exception class in order to make exception enrichment possible. Either that, or you'll have to wrap the caught exception in a new exception and throw the new exception.
