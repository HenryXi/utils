# Java Utility Classes

[![Build Status](https://travis-ci.org/RKumsher/utils.svg?branch=master)](https://travis-ci.org/RKumsher/utils) [![codecov](https://codecov.io/gh/RKumsher/utils/branch/master/graph/badge.svg)](https://codecov.io/gh/RKumsher/utils) [![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

Currently this library contains the following utility classes:
- [ArrayUtils](https://github.com/RKumsher/utils/blob/master/src/main/java/com/github/rkumsher/collection/ArrayUtils.java) - Utility library for working with Arrays
- [DateUtils](https://github.com/RKumsher/utils/blob/master/src/main/java/com/github/rkumsher/date/DateUtils.java) - Utility library for working with Dates
- [EnumUtils](https://github.com/RKumsher/utils/blob/master/src/main/java/com/github/rkumsher/enums/EnumUtils.java) - Utility library for working with Enums
- [IterableUtils](https://github.com/RKumsher/utils/blob/master/src/main/java/com/github/rkumsher/collection/IterableUtils.java) - Utility library for working with Iterables
- [RandomCollectionUtils](https://github.com/RKumsher/utils/blob/master/src/main/java/com/github/rkumsher/collection/RandomCollectionUtils.java) - Utility library to generate random collections
- [RandomArrayUtils](https://github.com/RKumsher/utils/blob/master/src/main/java/com/github/rkumsher/collection/RandomArrayUtils.java) - Utility library to generate random arrays
- [RandomDateUtils](https://github.com/RKumsher/utils/blob/master/src/main/java/com/github/rkumsher/date/RandomDateUtils.java) - Utility library to return random dates, e.g., Instants, ZonedDateTimes, LocalDates, Dates, etc.
  - Currently supports java.util.Date and all the dates, times, instants, and durations from Java 8's [date and time API](https://docs.oracle.com/javase/8/docs/api/java/time/package-summary.html)
- [RandomEnumUtils](https://github.com/RKumsher/utils/blob/master/src/main/java/com/github/rkumsher/enums/RandomEnumUtils.java) - Utility library to retrieve random elements from enum instances
- [RandomNumberUtils](https://github.com/RKumsher/utils/blob/master/src/main/java/com/github/rkumsher/number/RandomNumberUtils.java) - Utility library to return random numbers. Unlike Apaches RandomUtils, this supports negative numbers

## Example Usage
```java
@Test
public void managerWithFiveSubordinatesHasFavoriteEmployee() {
  Employee manager = createEmployee(JobTitle.MANAGER);
  manager.subordinates = RandomCollectionUtils.randomListFrom(this::createSubordinate, 5);
  Employee favoriteEmployee = IterableUtils.randomFrom(manager.subordinates);
  assertTrue(manager.subordinates.contains(favoriteEmployee));
}

private Employee createEmployee(JobTitle jobTitle) {
  Employee employee = new Employee();
  employee.jobTitle = jobTitle;
  employee.birthDateTime = RandomDateUtils.randomPastZonedDateTime();
  employee.startDate = RandomDateUtils.randomLocalDate();
  employee.endDate = RandomDateUtils.randomLocalDateAfter(employee.startDate);
  employee.clockInTime = RandomDateUtils.randomLocalTime();
  employee.clockOutTime = RandomDateUtils.randomLocalTimeAfter(employee.clockInTime);
  employee.lunchTime = RandomDateUtils.randomLocalTime(employee.clockInTime, employee.clockOutTime);
  employee.subordinates = Collections.emptyList();
  return employee;
}

private Employee createSubordinate() {
  JobTitle[] excludes = new JobTitle[] { JobTitle.MANAGER, JobTitle.SUPERVISOR };
  return createEmployee(RandomEnumUtils.random(JobTitle.class, excludes));
}

private class Employee {

  JobTitle jobTitle;
  ZonedDateTime birthDateTime;
  LocalDate startDate;
  LocalDate endDate;
  LocalTime clockInTime;
  LocalTime clockOutTime;
  LocalTime lunchTime;
  List<Employee> subordinates;
}

private enum JobTitle {
  MANAGER, SUPERVISOR, DEVELOPER, TESTER
}
```

## Where can I get the latest release?
You can download source and binaries from the [releases page](https://github.com/RKumsher/utils/releases).

Alternatively you can pull it from the central Maven repositories:

```xml
<dependency>
  <groupId>com.github.rkumsher</groupId>
  <artifactId>utils</artifactId>
  <version>1.3</version>
</dependency>
```

## License
This code is under the [Apache Licence v2](https://www.apache.org/licenses/LICENSE-2.0).
