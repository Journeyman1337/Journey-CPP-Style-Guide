<!--
SPDX-FileCopyrightText: 2023 Daniel Aimé Valcour <fosssweeper@gmail.com>

SPDX-License-Identifier: CC-BY-SA-4.0
-->

# The Journey C++ Style Guide v2.0.0
[![REUSE status](https://api.reuse.software/badge/git.fsfe.org/reuse/api)](https://api.reuse.software/info/git.fsfe.org/reuse/api)

Welcome to the Journey C++ Style Guide, a code formatting style guide designed for writing modern C++ in collaborative projects. Developed by Daniel Aimé Valcour (Journeyman-dev), this guide has been specifically tailored usage with [The Roguelike Framework (RLFW)](https://github.com/Journeyman1337/rlfw), but it released for public use under the [CC-BY-SA-4.0](https://creativecommons.org/licenses/by-sa/4.0/) license.

The Journey C++ Style Guide endeavors to utilize the cutting edge of the C++ Standard, and it takes into account the features of modern Integrated Development Environments (IDEs). By adhering to the guidelines outlined in this style guide, software projects can maintain a high level of consistency and facilitate collaboration. The sections of this guide are listed in no particular order.

The Journey C++ Style Guide uses the [Semantic Versioning](https://semver.org/) schema version 2.0.0. The style guide itself is located on [GitHub](https://github.com/Journeyman1337/Journey-Style-Guide).

## Salient Security

User security holds paramount importance. Always prioritize the usage of APIs designed to mitigate security vulnerabilities. When implementing code utilizing potentially unsafe APIs and features, exercise extra caution. Whenever possible, encapsulate unsafe code within a secure interface to minimize potential points where threat vectors could inadvertently be created. If you identify security risks that might not be apparent to other programmers, document them in comments. API documentation must explicitly explain the vulnerabilities programmers need to be mindful of. When selecting dependencies for specific tasks, libraries that are being actively developed and receive security updates must be preferred.

## Feature Preference

C++ has a rich legacy that goes back to the 1960s, and there are often may be many standard features available to accomplish the same task. When there are multiple ways of accomplishing the same task, the solution that came out in the most recent version of the C++ (or C) standard must be preferred because newer features are usually more secure and practical. However, older features may be used instead if there is a good reason for doing so. Comments must be used to explain this reasoning to others in order to prevent repeated discussion.

## Self Explaining Code

Clarity and comprehension are vital. Source code must be treated as a tutorial, serving as an educational resource to demonstrate how specific task can be accomplished. To facilitate understanding, incorporate explanatory comments in instances where the code is particularly intricate and may pose challenges for readers. However, redundant comments that merely restate obvious intentions or aspects of the code must be avoided, as they do not add value to the reader's understanding.

## Detailed Documentation

Function declarations must be preceded by comments that describe what the function does, what the arguments are for, and what is returned. Any potential security issues that a function can introduce if not used properly must be explained. Type declarations, including those for `class` types, `struct` types, and `concept` types, must be preceded by documentation comments that explain what the types are for and any potential security issues that may arise when using them incorrectly. Template declarations must also include comments that explain the purpose of each template argument. The styling of the documentation itself is up maintainers, but it must be consistent throughout each project. Consider using a documentation generator such as [Doxygen](https://www.doxygen.nl/).

## Explicit Licensing

Projects must be licensed following the [REUSE Software Specification](https://reuse.software/). The semantic version of the REUSE Software Specification used in a project must be clearly stated in a location that is easy to find.

## Explicit Generative AI Usage

If Artificial Intelligence was used to generate code, this must be described. This explanation can come in the form of comments that surround the block of code in question. If generative AI was used throughout a project, a single explanation may be provided in a single location that is easy to find. The explanation must include the official name of the generative AI tool, the version that was used, who created the AI, and a website url if available.

If project authors wish to forbid the usage of AI Code Generator in a project, this must be explicitly stated in a location that is easy to see.

## Explicit C++ Standard Version

The C++ standard version that a project targets must be explicitly stated in a location that is easy to find. Code in the project must never utilize features that were adopted in standards later than the one specified.

## Explicit Compiler Support

Code must only utilize C++ features that are supported by compilers where feature support is guaranteed by the project. Documentation as to what compilers and compiler versions are supported for must be provided in a location that is easy to find. Projects must be tested to ensure that it compiles successfuly with each supported compiler version.

## Explicit Project Versioning

Projects must be versioned [Semantic Versioning](https://semver.org/) schema version 2.0.0. The version of the project must be mentioned in a location that is easy to find. Notes about changes between versions must be included in the project, or a link to where they are located must be provided.

## Include Files

To prevent circular inclusion bugs, include files must include the statement `#pragma once` at the top of the file. While it is true that `#pragma once` is not a part of any C or C++ standard, it is supported by every significant compiler tool-chain including Clang, GCC, MSVC, and Emscripten.

C++ header files that users are meant to include must always end in the file extension `.hpp`. These files must never contain function implementations. Instead, functions must either be implemented in source files with the `.src` extension, or in "inline" include files with the `.inl` file extension in a sub-folder named `detail`. Inline headers must be used for implementing inline and constexpr functions, and must be included at the end of their associated `.hpp` files.

## Forward Declarations

Include files must include as few other include files as possible. In header files, which must have declarations only, favor forward declarations over includes in order to prevent circular dependency bugs from being introduced and decrease the size of included text. Remember: the more text that is included, the slower the code will compile. If too much code is included, it may cause other issues such as broken code completion.

## No Modules

C++ modules are not widely supported yet across all compilers, so projects must provide support for development without them. Expect this rule to change in the future when support is more widely available. Experimental module support may be included in a project, but the fact that it is experimental needs to be made clear.

## Descriptive Naming

Everything that can be named in the code, including variables and types, must be named descriptively rather than concisely. Code completion features prevalent in modern IDEs make it easy to type long variable names, so typing efficiency is not an issue here. However, names must not be too long either, and they must only be as descriptive as necessary for others to understand the code. It is up to programmers to use their best judgment as to what the best names for things should be. Names must never be longer than 25 characters.

## Name Casing

Names must be written in specific casing style depending on the situation.

* `enum` and `enum class` types must be named in PascalCase.
* `enum` and `enum class` values must be named in PascalCase.
* `class` types must be named in PascalCase.
* `struct` types must be named in underscore_case.
* Global functions must be named in underscore_case.
* Public member functions of `class` types must be named in PascalCase.
* All `struct` and `class` properties must be named in underscore_case.
* Local variables must be named in underscore_case.
* `private` and `protected` member functions of `class` types must be named in camelCase.
* Constant variables must be named in CAPS_CASE.
* Template arguments must be named in CAPS_CASE.
* Macros must be named in CAPS_CASE.
* `concept` and other type definitions must be named in underscore_case.
* Namespaces must be named in underscore_case.

## Hungarian Notation

Hungarian notation must be used in the specific circumstances which have been identified as potentially confusing. It must not be used in any situation other than what is listed here.

* Template arguments that accept types must be named ending with "_TTARG".
* Template arguments that accept values must be named ending with "_TARG".
* `concept` types must be named ending with "_concept" and must never be given a name that starts with a verb.
* Using assigned types (i.e. `using my_type = int;`) that are nested in `class` or `struct` types must end in "_t".
* Type trait `struct` types must be named ending with "_type_trait".
* When creating a type definition to quickly get the type of a type trait `struct`, it must end in "_t".
* Variables that contain an `std::optional` must be named ending with "_o".
* Variables that contain an `std::variant` must be named ending with "_v".
* Variables that contain an `std::expected` must be named ending with "_e".
* Variables that store a numeric index into a data structure must be named ending with "_i".

## Acronym Conventions

When naming things, long-form words must be used rather than acronyms. However, there are several exceptions this this rule:

* Namespaces may be named using acronyms or shortened words.
* Acronyms may be used to describe coordinate spaces or color channels, such as "stpq," "uv,", "xyz", "rgba," or "hsv." If something named in this way is meant to be used in non-generic situations, then an acronym alone may not be enough.
* Acronyms are acceptable when referring to an external library that is named using an acronym.

Additionally, when capitalizing acronyms in PascalCase or camelCase, it is required to capitalize only the first letter.

## Namespaces

Everything declared must be within a global namespace per project. The namespace name must be short but also reasonably unique compared to other existing libraries. Nested namespaces may be used to define customization points or to group things together.

Both declarations and implementations must be within a namespace block with braces. Namespaces for implementations may not be written in the type name of the implementation itself.

## Indents and Whitespace

Indents must be composed of two spaces. Tabs must never be used, because the physical length of tabs are inconsistent across different IDE's and code viewing applications. There must be no trailing whitespace characters at the end of lines. Words in code on the same line must be separated by only one space unless the programmer adds extra spaces in order to line list items in a table format for easy viewing.

## Empty Lines

Empty lines may be inserted anywhere in code in order to visually separate code into regions or blocks. However, there must never be more than one empty line in a row. There must be no trailing empty lines at the beginning or end of a file.

## Newlines

Lines must not be longer than 80 characters. A statement longer than 80 characters must be split into multiple lines. When a statement is split into multiple lines, each line after the first must be indented. For most binary operators, Line splits must never occur before they are written. However, for the dot (`.`) operator, line splits can only occur before the operator and never after.

If a function with arguments or is split into multiple lines, the arguments must be indented. There must be a newline after each comma that separates arguments and also after the last argument. The opening parenthesis of a split function must be on the same line as the function name, and the closing parenthesis must be on its own line or only with the statement terminating semicolon.

If an initializer list is split into multiple lines, the items must be indented. The opening brace must be on its own line. Multiple items can be written on the same line, but this must be consistent throughout the list. The closing brace must be on its own line or only with the statement terminating semicolon.

Multiple statements should never be written on the same line.

## Scopes

Empty scope bracket pairs may be written as `{}` and do not need to be written on a new line. However, for scopes that contain statements, the surrounding brackets must each be on their own lines. The statements within a scope must be indented, but the brackets themselves must not be.

## Constructor Initializer Lists

Constructor initializer lists must be written in the following style:

    PersonClass::PersonClass(std::string_view name, int age) noexcept
    : name(name)
    , age(age)
    {}

## Safe Destructors

User defined `class` and `struct` destructors must always be `noexcept`. If a potential error may occur during object destruction, they must be handled without an error.

## Source Characters

Source code must be written only using [ASCII characters](https://en.wikipedia.org/wiki/ASCII). Escape sequences must be used to write non-ASCII characters within string literals.

## Trailer Comments

The closing braces of namespaces must always contain a comment with the namespace declaration (i.e. `} // namespace my_namespace`). In conditional statements, `else` statements must always be followed by a commented condition that must be true if the `else` statement is ever reached (i.e. `else // if (value > 4)`). The same must be done for `#else`  pre-processor directives.

## Avoid Macro Magic

Macros may be used for switching out code based on project configuration and the platform. Macros must not be used in place of functions, and macros must not be used to generate complicated code. However, macros may be used in place of functions that must be written differently or ignored depending on project configuration or platform. XMacros must never be used. If the API of a dependency requires the use of generative macros, use them with extreme care and use them as little as necessary.

## Use Concepts Over SFINAE

When targeting versions of the C++ Standard that support `concept` types, they should always be used instead of Substitution Failure Is Not An Error (SFINAE) pattern. The SFINAE pattern results in confusing compiler error messages, while `concept` types are much more clear. Also, code written using the SFINAE pattern can be hard to maintain because of its increased complexity (see [Avoid Macro Magic](#avoid-macro-magic)).

## Use Concepts Over Requires

When using `requires` expressions, prefeer encapsulating constraints within `concept` types rather than having `requires` expressions attatched to object and function definitions. Consider the following template function implementation:

    #include <type_traits>

    template<typename TTARG>
        requires std::is_integral_v<TTARG>
    TTARG add(TTARG number_a, TTARG number_b)
    {
        return number_a + number_b;
    }

Instead of adding the requires keyword, the function would be far more concise if the template argument used a `concept` type for constraints.

    #include <concepts>

    template<std::integral TTARG>
    TTARG add(TTARG number_a, TTARG number_b)
    {
        return number_a + number_b;
    }

## Compiler Warnings

Compiler warnings must be treated as bugs that need to be fixed as soon as possible. To address compiler warnings, code may be edited to stop the warning, or the warning can be silenced if it is deemed as not a problem. Warnings must only be silenced narrowly around the offending code blocks rather than throughout an entire project. Before developers can silence a warning, they must receive a second opinion from an expert programmer to verify that there is no security vulnerability. Warnings only matter if they are reported from supported compilers (see [Explicit Compiler Support](#explicit-compiler-support)).

## Local Functions

Functions that are meant to be encapsulated within a translation unit must not use the static keyword. Instead, they must exist within anonymous namespaces. If utilized within only one other function, local functions may be written as a lambda assigned to a local variable instead.

## Default Qualifiers

Unless mutability is required, variables and member functions must have the const qualifier. Unless functions throw exceptions, they must have the noexcept qualifier by default.

## Accessibility Modifiers

In `class` and `struct` definitions, acessibility modifiers (`public`, `private`, etc) must be explicitly defined.

## Property Accessibility

`struct` types must only have `public` properties, while `class` types must only have have `private` and `protected` properties. However, `class` types may have `public` `const` properties and type definitions.

## Nested Types

The nesting of object type declarations within other object type declarations must be avoided in most circumstances in order to prevent circular reference issues. However, nesting of object type declarations is allowed for situations where the nested type must never be referenced by any other object declaration by the means of member function arguments, properties, type definitions, or otherwise.

## Null Pointers

When writing a null pointer value, the C++ `nullptr` keyword must be preferred. However, API specific notation may be used instead when working with other libraries, and the `NULL` macro from libc may be used when dealing with C APIs. Null pointer values must never be written as the literal "0" (see [Feature Preference](#feature-preference)).

## Void Function Arguments

Functions with no arguments must not include the `void` keyword in place of the arguments. This has no effect in C++ and is only relevant for C APIs, which is beyond the scope of this guide.

## View and Span Type Arguments

When passing strings as an argument to a function, prefer using `std::string_view` or a similar string viewing type from the standard library. When accepting array collections as a function argument, prefer `std::span` if possible. When creating custom contiguous collections, consider creating custom view or span types, or making your collection implicitly convertible to `std::span`.

## Safe Casting

When casting a value from one type to another, `reinterpret_cast()`, `dynamic_cast()`, `const_cast()`, or C style casts by never be used in any circumstance. The casts `static_cast()` and `std::bit_cast()` must be used instead.

## Conversions of User Types

Avoid implementing operators and constructors that allow for implicit conversions from one type to another unless the conversion is "cost-less". A conversion is cost-less if nothing is done other than value assignments. If a conversion is not cost-less, users must explicitly cast objects from one type to another. This may be done through a member function or a global function that does the conversion.

## Heap Memory Ownership

When dealing with memory allocated on the heap, ownership must be encapsulated into object lifetime to employ the Resource Acquisition Is Initialization (RAII) pattern. STL types that manage memory must be preferred over manual memory management, including `std::vector` and `std::unique_ptr`. The operators `new` and `delete` must not be used unless controlling memory allignment. C standard library memory functions such as `malloc`, `realloc` and `free` must never be used unless they are required (see [Feature Preference](#feature-preference)).

## Memory Reservation

When a contiguious heap allocated data structure is filled with data, the required memory must be allocated ahead of time if possible. This is far more optimal than gradually reallocating and expanding the memory as the data is filled. If the size can not be easily determined ahead of time, the memory must instead be reserved to the maximum possible minimum size and then shrunk down after the memory is filled. The template type `std::vector` from the standard library has built in functions for doing this. Custom user defined types that deal with heap memory must be declared simillar member functions to allow for this kind of optimization.

## Safe Memory Access

When values are indexed from an array, safeguards must exist to prevent segmentation faults from out of range access. When invalid access is possible at runtime, invalid access must be handled with a thrown exception, a returned `std::expected`, or some other method that is described in the documentation. When array access must be guaranteed at runtime to never go out of bounds, invalid access must be detected it in debug builds using an `assert()` statement.

## TODO Comments

Comment starting with the word `TODO` in all caps can be used to signify something that needs to be adjusted or added at a later time. If there is a specific time when the changes need to be made, such as for a specific future version, this should be specified in the comment.

    // TODO Optimize memory usage.
    // TODO Add a specific bit of new functionality by version 1.2

## Clear Line of Execution

Language features and hacks that break the clear line of code execution should be avoided. The `goto` statement should never be used. Jump buffers should never be used unless they are required by a third party API. In this case, it is important to encapsulate the jump buffer usage as much as possible in order to minimize its reach (see [Feature Preference](#feature-preference)). Throwing and catching exceptions does not go against this guideline.

## Minimize Nesting

Within functions, code should be written with as little nesting as possible. When there are m Consider inverting your conditional statements. Consider how errors are handled in the following code:

    void my_function(int value)
    {
        if (value > 0)
        {
            do_something(value);
        }
        else
        {
            throw InvalidValueException();
        }
    }

The condition statement can be inverted in order to remove the nesting. If an `if` block returns or throws, then all following `else` statements are no longer necessary. An added benefit of writing code in this style is that all conditions that cause errors or a fast return become easily visible at the start of the function.

    void my_function(int value)
    {
        if (value <= 0)
        {
            throw InvalidValueException();
        }

        do_something(value);
    }

Another way to minimize nesting is to move nested blocks into their own functions. To keep the logic encapsulated, blocks can be written as lambdas stored in local variables within the function.

