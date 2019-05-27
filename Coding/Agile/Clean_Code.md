# Clean Code - Robert C. Martin

## References and future reading

- Agile Software Development: Principals, Patterns, and Practices (PPP)

## Foreword

5S philosophy

- Seiri (Organization, sort)
- Seiton (Tidiness, a place for everything)
- Seiso (Cleaning, shine!)
- Seiketsu (standardization)
- Shutsuke (discipline)

> Cleanliness is next to godliness.

> He who is faithful in little is faithful in much.

> A stitch in time saves nine.

> The early bird catches the worm.

> An apple a day keeps the Dr away.

> An ouce of prevention is worth a pound of cure. 

> A bad penny always shows up.

"We abandon our code early, not because it is done, but because our value system focuses more on outward appearance than on the substance of what we deliver."

---

## Chapter 1 - Clean Code

LeBlanc's law: Later equals never.

The only way to make the deadline--the only way to go fast--is to keep the code as clean as possible at all tiems.

One broken window starts the process of decay.

Clean code is focused. Each function, each class, each module exposes a single-minded attitude taht remains entirely undistracted, and unpolluted, by the surrounding details.

If it hath not tests, it be unclean.

### Simple code

- Runs all the tests;
- Contains no dupliation;
- Expresses all the design ideas that are in the system;
- Minimizes the number of entities such as classes, methods, functions, and the like.

Authors are responsible for communicating well with their readers.

Leave the campground cleaner than you found it.

---

## Chapter 2 - Meaningful Names

- Use Intention-Revealing Names
- Avoid Disinformation
- Make Meaningful Distinctions
- Use Pronouncable Names
- Use Searchable Names
- Avoid Encodings
- Avoid Mental Mapping
- Class Names
- Method Names
- Don't Be Cute
- Don't Pun
- Use Solution Domain Names
- Use Problem Domain Names
- Don't Add Gratuitous Context

### Use Intention-Revealing Names (pg. 18)

> If a name requies a comment, then the name does not reveal its intent.

### Avoid Disinformation (pg. 19)

Names like `accountsList` are misleading because some languages use `List` types.

### Make Meaningful Distinctions (pg. 20)

Avoid:

- Changing `class` to `kclass` simplty because the former exists already
- Series naming (a1, a2, a3)
- Uninteligable argument names `arg1`, `arg2`
- Noise words (ProductInfo, ProductData)
- table, list, button, aned etc.

### Use Pronoucable Names (pg. 21)

genymdhms to generationTimestamp is easier to read.

Programming is a social activity so don't slow it down with words you can't say.

### Use Searchable Names (pg. 22)

Compare `NUMBER_OF_TASKS` to `n`

### Avoid Encodings (pg. 23)

Don't add to the noise.

### Avoid Mental Mapping (pg. 25)

Professional programmers understand that *clarity is king*.

### Class Names (pg. 25)

Classes and objects should have noun or noun phrase names like Customer, WikiPage, Account, and AddressParser.

> Avoid: Manager, Processor, Data, or Info. The class name should not be a verb.

### Method Names (pg. 25)

Use verbs or verb phrases. postPayment, deletePage, or save.

Overloaded constructors should use static factory methods with names that describe the arguments.

```java
Complex fulcrumPoint = Complex.FromRealNumber(23.0);
```

### Don't Be Cute (pg. 26)

Choose clarity over entertainment value.
Say what you mean. Mean what you say.

### Pick One Word per Concept (pg. 26)

Have consisten meaning and a consisten lexicon.

### Don't Pun (pg. 26)

Don't use a word to mean multiple things.

ex: `add` to create an array from two things vs `add` to insert something into an array.

### Use Solution Domain Names (pg. 27)

Choose techincal names for things when appropriate.

### Use Problem Domain Names (pg. 27)

When a technical name does not apply then reach for a name from the problem domain.

Give names context according to their class, function, or namespace.

### Don't Add Gratuitous Context (pg. 30)

Project name prefixes add unnecessary complexity.

`GSDAccountAddress`

Shorter names are better as long as they are clear.

---

## Chapter 3 - Functions