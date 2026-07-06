# Length_bytes notes
- daft/common/src/error.rs (contains DaftResult -> Acts like Result enum from Rust but includes custom Daft errors)

- cargo.toml -> contains all the dependecies of the Rust cargo package. I will be working with the daft-utf8 package that contains rust files that represent string functions that can be applied to an expression (aka column) of the DataFrame.

- ScalarUDF is a Rust trait that defines how a scalar function should behave. It tells Daft three things: what the function is called (name). How to validate its inputs and output type (get_return_field), and how to actually compute the result.

- unary_utf8_evaluate (checks if argument is there and checks if the whole column is null, if not then it runs the function)

- unary_utf8_to_field (checks for one input, checks for null column, checks if the column is a string column and returns the name and return datatype (either null or string))

- function_args normalizes the arguments no matter the front end( SQL, python, etc.), puts unnamed args before named args.

