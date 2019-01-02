# SQL Injection

## Concepts

- HTTP Post request
- Normal code analysis
- UPDATE
- SELECT, WHERE
- FROM
- DROP

## Attacks

- Remote code execution
- Availability
- Bypass auth ("ADMIN'--")
- Info disclosure
- Data integrity
- Password grabbing
- Transfer Whole DB
- OS Interatction

## Tests

1. Does DB Exist
2. List fields
3. Injection tests
4. Test input validation
5. Untion
6. Error MSGS

## Attack Characters

' or " (String Indicators)
-- or # (Comment)
/*....*/ (Multi line content)
+ (Addition)
|| (Pipes)
% (Wildcards)
AND 1=1--
ORDER BY

## Injection Types

- Blind (No erros, wair for...)
- SIMPLE (' or 1=1--)
- UNION (Combining from another table)
- ERROR

## Tools

- BSQLHACKER
- SQL Power Injector
- Havij

## Advanded

IF (ASCII(LOWER(SUBSTRING(USER), 1, 1))) = 97)
IF (ASCII(LOWER(SUBSTRING(USER), 2, 1))) = 98)
IF (ASCII(LOWER(SUBSTRING(USER), 3, 1))) = 99)
IF (ASCII(LOWER(SUBSTRING(USER), 4, 1))) = 100)

WAIT FOR DELAY '00:00:10'--

## Evasion

- Obfuscation
- Hex encoding
- Base64
- Inline comments
- Char()

## Countermeasures

- Minimum privileges
- No XP_CMDSHELL
- Suppress erros
- Custom errors
- Monitor the DB
- Filter content
- Test your code
- URL SCAN
- Snort Rules