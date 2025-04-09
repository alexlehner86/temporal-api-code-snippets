# Temporal API: Code Snippets
Code snippets for working with the new Temporal API in JavaScript. At the moment, only works in Firefox Nightly! Mozilla plans to [ship the feature in Firefox 139](https://groups.google.com/a/mozilla.org/g/dev-platform/c/RtsRo93ygO4/m/2YzM42GUBwAJ). Implementation in other browsers is still in progress.

## Temporal.PlainDate

### Create a new plain date object
```
let calendarDate = new Temporal.PlainDate(2025, 4, 9);
// output: Temporal.PlainDate 2025-04-09
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
calendarDate.toLocaleString("en-US"); // "4/9/2025" 
calendarDate.toLocaleString("de-AT"); // "9.4.2025"
calendarDate.toLocaleString("de-AT", { dateStyle: "full" }); // "Mittwoch, 9. April 2025" 
```

## Temporal.PlainTime

asdf

## Temporal.PlainDateTime

asdf
