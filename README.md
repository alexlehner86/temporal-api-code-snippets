# Temporal API: Code Snippets
Code snippets for working with the new Temporal API in JavaScript. At the moment, only works in Firefox Nightly! Mozilla plans to [ship the feature in Firefox 139](https://groups.google.com/a/mozilla.org/g/dev-platform/c/RtsRo93ygO4/m/2YzM42GUBwAJ). Implementation in other browsers is still in progress.

## Temporal.PlainDate

### Create a new plain date object
```
let calendarDate = Temporal.PlainDate.from("2021-01-01"); // "2021-01-01"
calendarDate = new Temporal.PlainDate(2025, 4, 9); // "2025-04-09"
```

### Access parts of the date
```
calendarDate.day; // 9
calendarDate.dayOfWeek; // 3
calendarDate.month; // 4
calendarDate.year; // 2025 
```

### Formatting: Create a language-sensitive representation of the date
```
let calendarDate = new Temporal.PlainDate(2025, 4, 9); // "2025-04-09"
calendarDate.toLocaleString("en-US"); // "4/9/2025" 
calendarDate.toLocaleString("de-AT"); // "9.4.2025"
calendarDate.toLocaleString("de-AT", { dateStyle: "full" }); // "Mittwoch, 9. April 2025"
calendarDate.toLocaleString("en-US", { year: "numeric", month: "long" }); // "April 2025" 
```

### Adding/subtracting duration
```
let calendarDate = new Temporal.PlainDate(2025, 4, 9); // "2025-04-09"
let newDate = calendarDate.add({ weeks: 5 });
newDate.toString(); // "2025-05-14"

newDate = newDate.subtract({ years: 2, days: 50 });
newDate.toString(); // "2023-03-25"

const duration = Temporal.PlainDate.from("2020-01-01").until("2021-03-15"); // 439 days
newDate = newDate.add(duration);
newDate.toString(); // "2024-06-06" 
```

### Compare plain dates
```
let calendarDate = new Temporal.PlainDate(2025, 4, 9); // "2025-04-09"
let otherDate = new Temporal.PlainDate(2025, 6, 5);  // "2025-06-05"
calendarDate.equals(otherDate); // false

Temporal.PlainDate.compare(calendarDate, otherDate); // -1 (means: is before)
Temporal.PlainDate.compare(otherDate, calendarDate); // 1 (means: is after)
Temporal.PlainDate.compare(otherDate, otherDate); // 0 (means: is equal)
```

## Temporal.PlainTime

asdf

## Temporal.PlainDateTime

asdf
