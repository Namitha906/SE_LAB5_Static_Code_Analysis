# Lab 5: Static Code Analysis — Reflection

## 1. What is static code analysis?

Static code analysis is the process of examining source code without executing the program to identify potential bugs, security vulnerabilities, and coding-standard violations. It helps developers detect problems early in the development process.

## 2. What is the purpose of Pylint, Bandit, and Flake8?

- **Pylint:** Evaluates Python code quality, naming conventions, documentation, and potential programming errors.
- **Bandit:** Identifies potentially insecure coding patterns and security risks.
- **Flake8:** Checks Python code for style violations, formatting issues, and other linting errors.

Using all three tools provides a more comprehensive assessment because each focuses on different aspects of code quality and security.

## 3. What issues were identified in the assigned program?

The original `music_catalog.py` program contained SQL query construction using string formatting, unsafe pickle deserialization, a mutable default argument, a bare exception handler, non-standard function names, missing docstrings, and formatting violations. Bandit reported four findings, Flake8 reported seven violations, and Pylint assigned the code a score of 4.57/10.

## 4. How were the identified issues resolved?

The SQL statement was changed to use parameterized queries. Pickle serialization was replaced with JSON, and `random.choice()` was replaced with `secrets.choice()`. The mutable default argument was changed to `None`, exception handling was made more specific, and the function names and documentation were improved. Long lines and multiple statements on one line were also corrected.

## 5. What were the results after fixing the issues?

After the modifications, Pylint assigned a score of 10.00/10, Bandit reported no issues, and Flake8 produced no violations. The program continued to execute successfully and produced the expected demonstration output.

## 6. What did you learn from this lab?

I learned that static analysis tools can identify issues that may not be immediately obvious during normal program execution. I also learned that code quality involves more than making a program work: security, readability, maintainability, error handling, and adherence to coding standards are important. Running the tools again after making changes helped verify that the reported issues had been resolved.

## Conclusion

This lab demonstrated how Pylint, Bandit, and Flake8 complement each other in improving Python code. Applying their findings made the music catalog program cleaner, more maintainable, and less vulnerable to common insecure coding patterns.