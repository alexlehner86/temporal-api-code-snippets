# Temporal API: Code Snippets

Code snippets for working with the new [Temporal API](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Temporal) in JavaScript, which enables date and time management in various scenarios. At the moment, only works in Firefox Nightly!

Mozilla plans to [ship the feature in Firefox 139](https://groups.google.com/a/mozilla.org/g/dev-platform/c/RtsRo93ygO4/m/2YzM42GUBwAJ). Implementation in other browsers is still in progress ([Chromium](https://issues.chromium.org/issues/42201538), [WebKit/Safari](https://bugs.webkit.org/show_bug.cgi?id=223166)).

## Temporal.PlainDate

### Create a new plain date object
```
let calendarDate = Temporal.PlainDate.from("2021-01-01"); // "2021-01-01"
calendarDate = new Temporal.PlainDate(2025, 4, 9); // "2025-04-09"
```

### Access parts of the plain date object
```
let calendarDate = Temporal.PlainDate.from("2025-04-09");
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

### Adding/subtracting duration to/from date
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

### Create a new plain time object
```
let t1 = Temporal.PlainTime.from("12:29:20.105"); // "12:29:20.105"
t1 = new Temporal.PlainTime(14, 55, 10, 250); // "14:55:10.25"
```

### Access parts of the plain time object
```
let t1 = Temporal.PlainTime.from("14:55:10.25");
t1.hour; // 14
t1.minute; // 55
t1.second; // 10
t1.millisecond; // 250
t1.microsecond; // 0
t1.nanosecond; // 0 
```

### Formatting: Create a language-sensitive representation of the time
```
let t1 = new Temporal.PlainTime(14, 55, 10, 250); // "14:55:10.25"
t1.toLocaleString("en-US"); // "2:55:10 PM"
t1.toLocaleString("de-AT"); // "14:55:10"
t1.toLocaleString("de-AT", { timeStyle: "short" }); // "14:55"
t1.toLocaleString("en-US", { hour: "2-digit" }); // "02 PM"
```

### Adding/subtracting duration to/from time
```
let t1 = new Temporal.PlainTime(14, 55, 10, 250); // "14:55:10.25"
let t2 = t1.add({ seconds: 5000 });
t2.toString(); // "16:18:30.25" 

t2 = t2.subtract({ hours: 5, minutes: 48 }); 
t2.toString(); // "10:30:30.25" 

const duration = Temporal.PlainTime.from("00:00:00").until("02:15:30"); // 2 hours, 15 minutes, 30 seconds
t2 = t2.add(duration);
t2.toString(); // "12:46:00.25"
```

### Compare plain times
```
let t1 = new Temporal.PlainTime(14, 55, 10, 250); // "14:55:10.25"
let t2 = Temporal.PlainTime.from("12:29:20.105"); // "12:29:20.105"
t1.equals(t2); // false

Temporal.PlainTime.compare(t1, t2); // 1 (means: is after)
Temporal.PlainTime.compare(t2, t1); // -1 (means: is before)
Temporal.PlainTime.compare(t2, t2); // 0 (means: is equal)
```

## Temporal.PlainDateTime

### Create a new datetime object
```
let datetime = Temporal.PlainDateTime.from("2020-10-15T08:30:00"); // "2020-10-15T08:30:00"
datetime = new Temporal.PlainDateTime(2025, 4, 30, 8, 25); // "2025-04-30T08:25:00"
```

### Access parts of the datetime object
```
let datetime = Temporal.PlainDateTime.from("2025-04-30T08:25:00");
datetime.year; // 2025
datetime.month; // 4
datetime.day; // 30
datetime.dayOfWeek; // 3
datetime.hour; // 8
datetime.minute; // 25
datetime.second; // 0
datetime.millisecond; // 0
datetime.microsecond; // 0
datetime.nanosecond; // 0 
```

### Formatting: Create a language-sensitive representation of the datetime
```
let datetime = new Temporal.PlainDateTime(2025, 4, 30, 8, 25); // "2025-04-30T08:25:00"
datetime.toLocaleString("en-US"); // "4/30/2025, 8:25:00 AM"
datetime.toLocaleString("de-AT", { dateStyle: "full", timeStyle: "short" }); // "Mittwoch, 30. April 2025 um 08:25"
```

## Temporal.Instant

### Create a new instant object
```
let instant1 = Temporal.Instant.fromEpochMilliseconds(1744198593000); // "2025-04-09T11:36:33Z"
let instant2 = new Temporal.Instant(1744199062000000000n); // "2025-04-09T11:44:22Z"; equivalent to Temporal.Instant.fromEpochNanoseconds()
let instant3 = Temporal.Instant.from("2022-07-10T12:00Z"); // "2022-07-10T12:00:00Z"
let instant4 = Temporal.Instant.from("2023-01-01T15+01:00"); // "2023-01-01T14:00:00Z"
```

### Access parts of the instant object
```
let instant1 = Temporal.Instant.fromEpochMilliseconds(1744198593000); // "2025-04-09T11:36:33Z"
instant1.epochMilliseconds; // 1744198593000
instant1.epochNanoseconds; // 1744198593000000000n 
```

### Formatting: Create a language-sensitive representation of this instant
```
let instant1 = Temporal.Instant.fromEpochMilliseconds(1744198593000); // "2025-04-09T11:36:33Z"
// toLocaleString() automatically uses current timezone of browser (in this case: UTC+2)
instant1.toLocaleString("en-US"); // "4/9/2025, 1:36:33 PM"
instant1.toLocaleString("de-AT", { dateStyle: "full", timeStyle: "short" }); // "Mittwoch, 9. April 2025 um 13:36"
```

### Adding/subtracting duration to/from instant
```
let instant1 = Temporal.Instant.fromEpochMilliseconds(1744198593000); // "2025-04-09T11:36:33Z"
let instant2 = instant1.add({ hours: 20 });
instant2.toString(); // "2025-04-10T07:36:33Z" 

const duration = Temporal.Duration.from({ minutes: 30 }); // "PT30M"
instant2 = instant2.subtract(duration);
instant2.toString(); // "2025-04-10T07:06:33Z" 

// It's not possible to add or subtract days, months or years because the Temporal.Instant object has no defined time zone.
instant2 = instant2.add({ days: 20 });
// Uncaught RangeError: duration "days" property must be zero
```

### Compare two instants
```
let instant1 = Temporal.Instant.from("2022-07-10T12:00Z"); // "2022-07-10T12:00:00Z"
let instant2 = Temporal.Instant.from("2023-01-01T15+01:00"); // "2023-01-01T14:00:00Z"
instant1.equals(instant2);  // false

Temporal.Instant.compare(instant1, instant2); // -1 (means: is before)
Temporal.Instant.compare(instant2, instant1); // 1 (means: is after)
Temporal.Instant.compare(instant2, instant2); // 0 (means: is equal)
```

## Temporal.ZonedDateTime

### Create a new zoned datetime object

You need to use a [supported time zone string](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) to create a `Temporal.ZonedDateTime` object.

```
let datetime1 = Temporal.ZonedDateTime.from({ timeZone: "Europe/Vienna", year: 2025, month: 4, day: 9, hour: 14 }); // "2025-04-09T14:00:00+02:00[Europe/Vienna]" 
let datetime2 = Temporal.ZonedDateTime.from("2020-10-15T08:30Z[America/New_York]"); // "2020-10-15T04:30:00-04:00[America/New_York]"
let datetime3 = new Temporal.ZonedDateTime(1744198593000000000n, "Europe/Vienna"); // "2025-04-09T13:36:33+02:00[Europe/Vienna]"
```

You can also convert an instant or a plain datetime to a zoned datetime.

```
// Instant to ZonedDateTime
let instant = Temporal.Instant.fromEpochMilliseconds(1744198593000);
let datetime4 = instant.toZonedDateTimeISO("Europe/Vienna"); // "2025-04-09T13:36:33+02:00[Europe/Vienna]"
```
```
// PlainDateTime to ZonedDateTime
let plainDate = Temporal.PlainDateTime.from("2025-04-09T13:36:33");
let datetime5 = plainDate.toZonedDateTime("Europe/Vienna"); // "2025-04-09T13:36:33+02:00[Europe/Vienna]"
```

### Access parts of the zoned datetime object
```
let datetime = new Temporal.ZonedDateTime(1744198593000000000n, "Europe/Vienna"); // "2025-04-09T13:36:33+02:00[Europe/Vienna]"
datetime.year; // 2025
datetime.month; // 4
datetime.day; // 9
datetime.dayOfWeek; // 3
datetime.hour; // 13
datetime.minute; // 36
datetime.second; // 33
datetime.millisecond; // 0
datetime.microsecond; // 0
datetime.nanosecond; // 0
datetime.epochMilliseconds; // 1744198593000
datetime.epochNanoseconds; // 1744198593000000000n 
```

### Formatting: Create a language-sensitive representation of the zoned datetime
```
let datetime = Temporal.ZonedDateTime.from("2020-10-15T08:30Z[America/New_York]"); // "2020-10-15T04:30:00-04:00[America/New_York]"
datetime.toLocaleString("en-US"); // "10/15/2020, 4:30:00 AM EDT"

let datetimeInAustria = datetime.withTimeZone("Europe/Vienna"); // "2020-10-15T10:30:00+02:00[Europe/Vienna]"
datetimeInAustria.toLocaleString("de-AT", { dateStyle: "full", timeStyle: "short" }); // "Donnerstag, 15. Oktober 2020 um 10:30"
```

### Adding/subtracting duration to/from zoned datetime
```
let datetime = Temporal.ZonedDateTime.from("2025-01-12T08:45[Europe/Vienna]"); // "2025-01-12T08:45:00+01:00[Europe/Vienna]"
let newDatetime = datetime.add({ months: 7, weeks: 3 });
newDatetime.toString(); // "2025-09-02T08:45:00+02:00[Europe/Vienna]" 

newDatetime = newDatetime.subtract({ years: 2, days: 50 });
newDatetime.toString(); // "2023-07-14T08:45:00+02:00[Europe/Vienna]" 
```

### Compare zoned datetimes

The `Temporal.ZonedDateTime.prototype.equals()` method takes into account the instant and the time zone:
```
let datetime1 = Temporal.ZonedDateTime.from("2020-10-15T08:30Z[America/New_York]"); // "2020-10-15T04:30:00-04:00[America/New_York]"
let datetime2 = Temporal.ZonedDateTime.from("2020-10-15T10:30:00+02:00[Europe/Vienna]"); // "2020-10-15T10:30:00+02:00[Europe/Vienna]"
datetime1.equals(datetime2); // false
```

On the other hand, the `Temporal.ZonedDateTime.compare()` method only compares the instants:
```
Temporal.ZonedDateTime.compare(datetime1, datetime2); // 0 (means: is equal)
```

## Temporal.Now

### Get the current time in various formats

```
let instant = Temporal.Now.instant(); // "2025-04-10T08:51:50.74Z"
let plainDate = Temporal.Now.plainDateISO(); // "2025-04-10"
let plainTime = Temporal.Now.plainTimeISO(); // "10:53:05.676"
let plainDateTime = Temporal.Now.plainDateTimeISO(); // "2025-04-10T10:53:51.055"
let zonedDateTime = Temporal.Now.zonedDateTimeISO(); // "2025-04-10T10:54:22.579+02:00[Europe/Vienna]"
```

### Get the current time zone

```
let myTimezone = Temporal.Now.timeZoneId(); // "Europe/Vienna"
```

## Temporal.Duration

### Create a new duration object

```
let duration1 = new Temporal.Duration(1, 2, 4, 15, 20, 30); // P1Y2M4W15DT20H30M
let duration2 = Temporal.Duration.from({ hours: 1, minutes: 30 }); // "PT1H30M"
```

You can also create a duration with the combination of the `from` and `until` methods for date/time objects:

```
let duration3 = Temporal.PlainDate.from("2020-01-01").until("2021-03-15"); // "P439D"
let duration4 = Temporal.PlainTime.from("12:30").until("17:45"); // "PT5H15M"
let duration5 = Temporal.PlainDateTime.from("2025-02-02T12:30:22").until("2025-10-15T08:00:27"); // "P254DT19H30M5S"
```

### Manipulate a duration value

Rounding the duration to a specified unit:

```
let duration = Temporal.PlainTime.from("12:30").until("17:45"); // "PT5H15M"
duration = duration.round("hours"); // "PT5H"
```

When rounding date specific values (e.g. days), we need to provide a `relativeTo` date:

```
let duration = new Temporal.Duration(1, 2, 4, 15, 20, 30); // "P1Y2M4W15DT20H30M"
const relativeToDate = Temporal.PlainDateTime.from("2022-01-01");
duration = duration.round({ smallestUnit: "days", relativeTo: relativeToDate }); // "P1Y3M13D"
```

### Compare one duration to another

```
const duration1 = Temporal.PlainDate.from("2020-01-01").until("2021-03-15"); // "P439D"
const duration2 = Temporal.PlainDate.from("2020-05-10").until("2021-06-15"); // "P401D"
Temporal.Duration.compare(duration1, duration2); // 1  (means: duration1 is longer)
```

### Add a duration to a date, time, or datetime

```
let t1 = new Temporal.PlainTime(14, 55, 10, 250); // "14:55:10.25"
const duration = Temporal.PlainTime.from("00:00:00").until("02:15:30"); // 2 hours, 15 minutes, 30 seconds
t1 = t1.add(duration);
t1.toString(); // "17:10:40.25"
```

### Subtract a duration from a date, time, or datetime

```
let calendarDate = new Temporal.PlainDate(2025, 4, 9); // "2025-04-09"
const duration = Temporal.PlainDate.from("2020-01-01").until("2021-03-15"); // 439 days
calendarDate = calendarDate.subtract(duration);
calendarDate.toString(); // "2024-01-26"
```
