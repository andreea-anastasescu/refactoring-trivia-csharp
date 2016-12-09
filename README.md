# Refactoring Trivia

Exercise based on the [Trivia](https://github.com/caradojo/trivia) Legacy Code Retreat code.


# Steps

## Golden Master

* Capture the program's output and check whether it's deterministic or not;
* Repeat the execution a reasonable number of times, until the code coverage gives you enough confidence for your subsequent refactoring activities;
* Collect the output in a file, and include it in the test project, using an error-prone manual operation (Poka-yoke).

## Make the output deterministic

### Injecting pararameters via args
* Identify the source of non-determinism;
* Make it parametric and make the parameter controllable via args;
* Use parameters in tests to make them deterministic.

### Via Slice
* Identify the source of non-determinism;
* Extract it as a method;
* Make the method virtual, so it can be overridden in the tests; using inheritance make a test version of the productive code, which removes the non-deterministic behaviors;
* When needed, introduce non-static classes and replace the static program entry point with a non-static method.

### Via Peel
* Identify the source of non-determinism;
* Isolate it from the code, moving it to the top;
* Extract the rest of the code in a separate method, which takes the non-deterministic value as a parameter;
* Use the new method in the test, with a deterministic parameter.


## Refactor `Game`'s constructor: move question creation to a dedicated class
* Extract the business logic present in the constructor of `Game` to a separate method `FillQuestions()`
* Move `FillQuestions()` in a separate `QuestionDeck` class; `Game`'s constructor will create an instance of `QuestionDeck` and will store it as an instance field;
* Pass `FillQuestions()` the current instance of `Game` so it can stil access the needed fields. We will move them later;
* To achieve the previous step, encapsulate all the fields `FillQuestions()` needs to access, creating Bottlenecks.
* `FillQuestions()` also accesses another `Game`'s method, `createRockQuestion()`: move it to `QuestionDeck` as well;

