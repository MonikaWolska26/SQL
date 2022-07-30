# SQL

#### Math operators:

- addition +
- subtraction -
- division \
- multiplication *
- % modulo (returns the remainder)

#### Math functions:

- ABS(): returns the absolute value of the input expression
- CAST(expr as type-name): converts an expression into another data type

#### Date and time functions:

- DATETIME(): returns the date and time of a time string
- DATE(): returns the date portion of a time string
- TIME(): returns the time portion of a time string
- STRFTIME(): returns a formatted date

example:

	SELECT DATETIME('now', 'localtime');

The following modifiers can be used to shift the date backwards to a specified part of the date.
- start of year: shifts the date to the beginning of the current year.
- start of month: shifts the date to the beginning of the current month.
- start of day: shifts the date to the beginning of the current day.

	SELECT DATETIME(timestring, modifier1, modifier2, ...);

The following modifiers add a specified amount to the date and time of the time string.
- '+-N years': offsets the year
- '+-N months': offsets the month
- '+-N days': offsets the day
- '+-N hours': offsets the hour
- '+-N minutes': offsets the minute
- '+-N seconds': offsets the second

For example, we can have the following statement.

	SELECT DATETIME('2020-02-10', 'start of month', '-1 day', '+7 hours');

The STRFTIME() function allows you to return a formatted date, as specified in a format string.

	STRFTIME(format, timestring, modifier1, modifier2, ...)

- The first argument, format, is the format string.
- The second argument is the timestring.
- The remaining arguments are 0 or more optional modifiers to transform the time string.

The substitutions to extract each part of the date and time are the following:

- %Y returns the year (YYYY)
- %m returns the month (01-12)
- %d returns the day of month (01-31)
- %H returns the hour (00-23)
- %M returns the minute (00-59)
- %S returns the second (00-59)

For example, to extract the month and year of the current date,

	SELECT STRFTIME('%m %Y', 'now');

#### Formats of date

- Date: YYYY-MM-DD
- Datetime or Timestamp: YYYY-MM-DD hh:mm:ss

