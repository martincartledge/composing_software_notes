##### Pure Functions

Function

> a process which takes some input, called arguments, and produces some output called a return value

- Mapping

> Produce some output based on given inputs. A function maps input values to output values

- Procedures

> A function may be called to perform a sequence of steps

- I/O

> Some functions exist to communicate with other parts of the system, such as the screen, storage, system logs, or network

- Pure function

> Given the same input, will always return the same output.

> Produces no side effects.

Trouble with shared state

> Any sort of asynchronous operation or concurrency could cause similar race conditions. Race conditions happen if output is dependent on the sequence of uncontrollable events (such as network, device latency, user input, randomness, and so on).

> Non-determinism = parallel processing + mutable state

Referrentially transparent

> replace the expression with its corresponding value without changing the meaning of the program

> Pure functions can be used to optimize software performance. For instance, rendering a view is often an expensive operation, which can be skipped if the data underlying the view has not changed
