Input and output
================

All of mp++'s multiprecision classes support stream insertion:

.. code-block:: c++

   std::cout << int_t{42} << '\n';        // "42"
   std::cout << rat_t{-6, 7} << '\n';     // "-6/7"
   std::cout << real128{"1.1"} << '\n';   // "1.10000000000000000000000000000000008e+00"
   std::cout << real{"1.3", 150} << '\n'; // "1.3000000000000000000000000000000000000000000006"

Starting from mp++ 0.14, :cpp:class:`~mppp::integer` and :cpp:class:`~mppp::rational`
honour the format flags in output streams:

.. code-block:: c++

   #include <iomanip>
   #include <ios>

   std::cout << std::hex << std::showbase << int_t{42} << '\n'; // "0x2a"
   std::cout << std::oct << std::showbase << std::showpos
             << std::setw(10) << std::setfill('*')
             << int_t{42} << '\n';                              // "******+052"
   std::cout << std::hex << std::showbase << std::uppercase
             << rat_t{227191947ll, 13} << '\n';                 // "0XD8AAC8B/0XD"

In future versions of mp++, the floating-point classes will also honour the format flags in output streams.

All of mp++'s multiprecision classes also provide ``to_string()`` member functions that convert the multiprecision
values into string representations (see, e.g., :cpp:func:`mppp::integer::to_string()`, :cpp:func:`mppp::rational::to_string()`,
etc.). These member functions always return an "exact" string representation of the multiprecision value: feeding back
the string representation to a constructor from string will initialise a value identical to the original one.
