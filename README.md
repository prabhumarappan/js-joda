# js-joda-timezone

[![Greenkeeper badge](https://badges.greenkeeper.io/js-joda/js-joda-timezone.svg)](https://greenkeeper.io/)

[![npm version](https://badge.fury.io/js/js-joda-timezone.svg)](https://badge.fury.io/js/js-joda-timezone)
[![Build Status](https://travis-ci.org/js-joda/js-joda-timezone.svg)](https://travis-ci.org/js-joda/js-joda-timezone)
[![Sauce Test Status](https://saucelabs.com/buildstatus/js-joda-timezone)](https://saucelabs.com/u/js-joda-timezone)
[![Coverage Status](https://coveralls.io/repos/js-joda/js-joda-timezone/badge.svg?branch=master&service=github)](https://coveralls.io/github/js-joda/js-joda-timezone?branch=master)
[![Tested node version](https://img.shields.io/badge/tested_with-current_node_LTS-blue.svg?style=flat)]()

[![Sauce Test Status](https://saucelabs.com/browser-matrix/js-joda-timezone.svg)](https://saucelabs.com/u/js-joda-timezone)

## Motivation

bindings to the iana tzdb, using latest zone file generated by moment-timezone

## Usage

### Node

Install joda using npm

    npm install js-joda

Then require it 

    jsJoda = require('js-joda')
        .use(require('js-joda-timezone'))
    
    const {LocalDateTime, ZoneId, ZonedDateTime } = jsJoda;
    
    const zone = ZoneId.of('Europe/Berlin')
    const zdt = LocalDateTime.parse('2016-06-30T11:30').atZone(zone) // 2016-06-30T11:30+02:00[Europe/Berlin]
    ZonedDateTime.parse('2016-06-30T11:30+02:00[Europe/Berlin]')     // 2016-06-30T11:30+02:00[Europe/Berlin]
    zdt.withZoneSameInstant(ZoneId.of('America/New_York')) // 2016-06-30T05:30-04:00[America/New_York]
    zdt.withZoneSameLocal(ZoneId.of('America/New_York'))   // 2016-06-30T11:30-04:00[America/New_York]

### Browser

    <script src="../dist/js-joda.js"></script>
    <script src="../dist/js-joda-timezone.js"></script>
    <script>
        // use js-joda-timezone
        JSJoda.use(JSJodaTimezone)
 
        // copy all js-joda classes to the global scope
        for(let key in JSJoda) { this[key] = JSJoda[key]; }

        const zone = ZoneId.of('Europe/Berlin')
        let zdt = LocalDateTime.parse('2016-06-30T11:30').atZone(zone)
        console.log(zdt.toString()) // 2016-06-30T11:30+02:00[Europe/Berlin]

        zdt = ZonedDateTime.parse('2016-06-30T11:30+02:00[Europe/Berlin]')
        console.log(zdt.toString()) // 2016-06-30T11:30+02:00[Europe/Berlin]

        zdtl = zdt.withZoneSameInstant(ZoneId.of('America/New_York'))
        console.log(zdtl.toString())  // 2016-06-30T05:30-04:00[America/New_York]

        zdti = zdt.withZoneSameLocal(ZoneId.of('America/New_York'))
        console.log(zdti.toString()) // 2016-06-30T11:30-04:00[America/New_York]
    </script>

## Known Issues

The package is incomplete, has pure test coverage and work is in progress.

* ZoneDateTime methods should work correctly, except for calculations during a daylight saving 
  transition
* LocalDate.atStartOfDay(zone) might return wrong date if the start of day is within a daylight saving 
  transition. (very rare case like at gaza)
* ZoneRules only implement methods that are required by js-joda core, there is still functionality missing
* other ZoneRules methods (like standardOffset) are not supported  

## License

+ js-joda-timezone is released under the [BSD 3-clause license](LICENSE):

+ The author of joda time and the lead architect of the JSR-310 is Stephen Colebourne.
