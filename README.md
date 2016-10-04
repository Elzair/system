# boost.system

Error conditions originating from the operating system or other low-level application program interfaces (API's) are typically reported via an integer representing an error code. When these low-level API calls are wrapped in portable code, such as in a portable library, some users want to deal with the error codes in portable ways. Other users need to get at the system specific error codes, so they can deal with system specific needs. The Boost System library provides simple, light-weight [error_code](doc/reference.html#Class-error_code) objects that encapsulate system-specific error code values, yet also provide access to more abstract and portable error conditions via [error_condition](doc/reference.html#Class-error_condition) objects. Because **error_code** objects can represent errors from sources other than the operating system, including user-defined sources, each **error_code** and **error_condition** has an associated [error_category](doc/reference.html#Class-error_category).

An exception class, [system_error](doc/reference.html#Class-system_error) , is provided. Derived from **std::runtime_error**, it captures the underlying **error_code** for the problem causing the exception so that this important information is not lost.

While exceptions are the preferred C++ default error code reporting mechanism, users of libraries dependent on low-level API's often need overloads reporting error conditions via error code arguments and/or return values rather than via throwing exceptions. Otherwise, when errors are not exceptional occurrences and must be dealt with as they arise, programs become littered with try/catch blocks, unreadable, and very inefficient. The Boost System library supports both error reporting by exception and by error code.

In addition to portable errors codes and conditions supported by the `error_code.hpp` header, system-specific headers support the Cygwin, Linux, and Windows platforms. These headers are effectively no-ops if included for platforms other than their intended target.

> The Boost System Library is part of the C++11 Standard Library. A number of changes, particularly to names, were made by the C++ committee during standardization. The Boost implementation is tracking those changes. See [Deprecated names](doc/reference.html#Deprecated-names) for synonyms provided to prevent breakage of existing user code. See [Breaking changes](doc/reference.html#Breaking-changes) for changes that unavoidably break existing user code. All breaking changes are noisy and will cause compile-time errors.

## Boost Dependencies

[Boost.Assert](https://github.com/boostorg/assert)
[Boost.Config](https://github.com/boostorg/config)
[Boost.Core](https://github.com/boostorg/core)
[Boost.Predef](https://github.com/boostorg/predef)
