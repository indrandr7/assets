# Cendana15 MAGMA-VAR API

Cendana15 MAGMA-VAR API provides an endpoint to query Merapi observation data
through a web service.

## Endpoint

    GET /api/public/v1/magmavar

The following parameters can be optionally included in the URL query string:

| Parameter |                               Description                                |
| --------- | ------------------------------------------------------------------------ |
| date      | Observation date in YYYY-mm-dd format. Default to today's date.          |
| period    | Period ID to which time range observation data is queried. Default to 0. |

- `date` (String)

  It is the date where you want to query observation data in `YYYY-mm-dd`
  format. For example, `2022-02-10`, `2022-04-12`. If the value is not present
  in the URL query parameters, default value is today's date.

- `period` (Number)

  It is period ID to which time range you want to query observation data in the
  specified date. See table below for complete list:

  | Period ID |  Time Range   |
  | --------- | ------------- |
  | 0         | 00:00 - 24:00 |
  | 1         | 00:00 - 06:00 |
  | 2         | 06:00 - 12:00 |
  | 3         | 12:00 - 18:00 |
  | 4         | 18:00 - 24:00 |

  If period is not present in the URL query parameters, default value is 0.

  For example, query observation data for date `2022-02-10` and time range from
  `12:00` to `18:00`:

      GET /api/public/v1/magmavar?date=2022-02-10&period=3

## Example

Get observation data for today's date. For example, current date is
`2022-04-10`:

    GET /api/public/v1/magmavar

Example response:

```json
{
  "observationDate": "2022-04-10",
  "startTime": "2022-04-10 00:00:00",
  "endTime": "2022-04-11 00:00:00",
  "timezone": "Asia/Jakarta",
  "periodId": 0,
  "timeRange": "00:00-24:00",
  "periodText": "2022-04-10 00:00-24:00 WIB",
  "volcano": {
    "name": "Merapi",
    "elevation": 2968,
    "location": "Sleman, Magelang, Boyolali, Klaten, Daerah Istimewa Yogyakarta dan Jawa Tengah"
  },
  "meteorology": {
    "temperature": { "min": 17.5, "max": 25, "avg": 15.5 },
    "windSpeed": { "min": 0, "max": 6.1, "avg": 5.5, "level": "TENANG" },
    "windDirection": "BARAT",
    "humidity": { "min": 37, "max": 97.8, "avg": 55.5 },
    "pressure": { "min": 687, "max": 918, "avg": 788.3 },
    "rainfall": {
      "startTime": "2022-04-10 12:15:00",
      "endTime": "2022-04-10 14:30:00",
      "value": 11,
      "intensity": 0.2,
      "level": "RINGAN",
    },
    "weather": ["CERAH", "BADAI", "MENDUNG"]
  },
  "seismicity": [
    {
      "code": "VTB",
      "name": "Vulkanik Dangkal",
      "count": 2,
      "amplitude": { "min": 29, "max": 30 },
      "duration": { "min": 9.08, "max": 9.4 }
    },
    {
      "code": "MP",
      "name": "Hybrid/Fase Banyak",
      "count": 2,
      "amplitude": { "min": 3, "max": 5 },
      "duration": { "min": 6, "max": 7.2 }
    },
    {
      "code": "LF",
      "name": "Low Frekuensi",
      "count": 1,
      "amplitude": 13,
      "duration": 10
    },
    {
      "code": "ROCKFALL",
      "name": "Guguran",
      "count": 148,
      "amplitude": { "min": 3, "max": 37 },
      "duration": { "min": 13, "max": 169 }
    },
    {
      "code": "TECT",
      "name": "Tektonik Jauh",
      "count": 1,
      "amplitude": 3,
      "duration": 74.2
    }
  ],
  "shake": [4, 2],
  "visual": {
    "visibility": ["TAMPAK", "KABUT 03"],
    "smoke": {
      "color": "PUTIH",
      "intensity": "TEBAL",
      "pressure": "LEMAH",
      "direction": "BARAT",
      "height": 100,
      "occurredAt": "2022-04-10 05:55:00"
    },
    "ap": {
      "max_distance": 4000,
      "direction": "Bebeng",
      "count": 40
    },
    "rf": {
      "max_distance": 1000,
      "direction": "Bebeng",
      "count": 4
    }
  },
  "observer": [
    { "gid": "08", "nip": "196463282162311001", "name": "Supardan" },
    { "gid": "74", "nip": "196888623253731001", "name": "Suratman" }
  ],
  "photo": {
    "location": "Kaliurang",
    "url": "http://127.0.0.1:8000/storage/reports/62522ad44ba74kal.10092022 11.24.jpg",
    "takenAt": "2022-04-10 05:24:00"
  },
  "createdAt": "2022-04-10 07:52:03",
  "others": [
    {
      "description": "Penambahan aliran sungai di Kali Krasak",
      "occurredAt": "2022-04-10 09:50:00"
    }
  ],
  "activityLevel": {
    "level": 3,
    "status": "siaga",
    "date": "2020-11-05"
  },
  "recommendation": "1. Potensi bahaya saat ini berupa guguran lava dan awanpanas pada sektor selatan-barat daya meliputi Sungai Boyong sejauh maksimal 5 km, Sungai Bedog, Krasak, Bebeng sejauh maksimal 7 km. Pada sektor tenggara meliputi Sungai Woro sejauh maksimal 3 km dan Sungai Gendol 5 km. Sedangkan lontaran material vulkanik bila terjadi letusan eksplosif dapat menjangkau radius 3 km dari puncak.\n2. Masyarakat agar tidak melakukan kegiatan apapun di daerah potensi bahaya. \n3. Masyarakat agar mengantisipasi gangguan akibat abu vulkanik dari erupsi Gunung Merapi serta mewaspadai bahaya lahar terutama saat terjadi hujan di seputar G. Merapi.\n4. Jika terjadi perubahan aktivitas yang signifikan, maka status aktivitas Gunung Merapi akan segera ditinjau kembali."
}
```

Get observation data for custom date (`2022-10-14`) and period 2 (`06:00` -
`12:00`):

    GET /api/public/v1/magmavar?date=2022-10-14&period=2

## Response Data

All data send by backend is in JSON format. Successful reponse data would look
like in the example above.

For certain date and period combination, the backend may send empty JSON object.
This happens when there are no observation data or data may not be inputted yet
by our observers. The former case may happen if you query the date more than
today, or the date that are far away before today. For the later case, if the
time when you query data greater than certain observation period, you will most
likely get data you want.

For daily operations, our observers are periodically inputting observation data
to our systems in order to keep data continuity and updates.

## Field Reference

- `observationDate` (String)

  Observation date in the format of YYYY-mm-dd. It will equal to `date` value in
  the URL query parameter if provided. Example: `2022-10-10`.

- `startTime` (String)

  Start time of observation. Example: `2022-04-10 00:00:00`.

- `endTime` (String)

   End time of observation. Example: `2022-04-11 00:00:00`.

- `timezone` (String)

   Time zone name, i.e. `Asia/Jakarta`.

- `periodId` (Number)

  Period ID to which time range observation data queried. It will equal to
  `period` value in the URL query parameters if provided. Example: `0`, `1`,
  `2`.

- `timeRange` (String)

  Time range text of current observation. It only contains hour range. Example:
  `00:00-24:00`.

- `periodText` (String)

  Full observation time range text. It consists of current date and hour range.
  Example: `2022-04-10 00:00-24:00 WIB`.

- `volcano` (Object)

  Basic volcano information. It is an object containing the following fields:

  - `name` (String)

    Name of the volcano, i.e. Merapi.

  - `elevation` (Number)

    Elevation in meter above mean sea level, i.e. 2968 meters.

  - `location` (String)

    Location of the volcano, i.e. Sleman, Magelang, Boyolali, Klaten, Daerah
    Istimewa Yogyakarta dan Jawa Tengah

- `meteorology` (Object)

  Meteorology information in the current observation time range. It is an object
  containing the following fields:

  - `temperature` (Object | null)

    Air temperature data obtained from all observatory stations in degree
    Celcius. If there are no data in the current time range, the value would be
    `null`. If it an object, it contains the following:

    - `min` (Number)

      Minimum value of air temperature.

    - `max` (Number)

      Maximum value of air temperature.

    - `avg` (Number)

      Average value of air temperature.

    Example:

      ```json
      { "min": 10.5, "max": 25, "avg": 15.5 }
      ```

  - `pressure` (Object | null)

    Air pressure obtained from all observatory stations in mmHg. If there are no
    data in the current time range, the value would be `null`. If it an object,
    it contains the following:

    - `min` (Number)

      Mininum value of air pressure.

    - `max` (Number)

      Maximum value of air pressure.

    - `avg` (Number)

      Average value of air pressure.

    Example:

      ```json
      { "min": 687, "max": 918, "avg": 788.3 }
      ```

  - `humidity` (Object | null)

    Air humidity obtained from all observatory stations in percent (%). If there
    are no data in the current time range, the value would be `null`. If it an
    object, it contains the following:

    - `min` (Number)

      Minimum value of air humidity.

    - `max` (Number)

      Maximum value of air humidity.

    - `avg` (Number)

      Average value of air humidity.

    Example:

      ```json
      { "min": 37, "max": 97.8, "avg": 55.5 }
      ```

  - `windSpeed` (Object | null)

    Wind speed data obtained from all observatory stations in km/hour. If there
    are no data in the current time range, the value would be `null`. If it an
    object, it will contains the following:

    - `min` (Number)

      Minimum value of wind speed for current observation time range.

    - `max` (Number)

      Maximum value of wind speed for current observation time range.

    - `avg` (Number)

      Average value of wind speed for current observation time range.

    - `level` (String)

      Level of average wind speed value. Possible values are:

      |  Level  |
      | ------- |
      | TENANG  |
      | LEMAH   |
      | SEDANG  |
      | KENCANG |

    Example:

      ```json
      { "min": 0, "max": 6.1, "avg": 5.5, "level": "TENANG" }
      ```

  - `windDirection` (String | null)

    Most occurred wind direction obtained from all observatory stations. Below
    is the list of possible values:

    | Wind Direction |
    | -------------- |
    | TIMUR          |
    | TENGGARA       |
    | SELATAN        |
    | BARAT DAYA     |
    | BARAT          |
    | BARAT LAUT     |
    | UTARA          |
    | TIMUR LAUT     |

  - `rainfall` (Object | null)

    The highest occurrence of rainfall values obtained from all observatory
    stations. If there are no data in the current time range, the value would be
    `null`. If value is present, it will contain the following fields:

    - `startTime` (String)

      Start time when the rain happened, e.g. `2022-04-10 12:15:00`.

    - `endTime` (String)

      End time when the rain stopped, e.g. `2022-04-10 14:30:00`.

    - `value` (Number)

      Rainfall value in mm.

    - `intensity` (Number)

      Rainfall intensity value in mm/hour.

    - `level` (String)

      The rainfall level based on BMKG rainfall category. Possible values are:

      |    Level     |
      | ------------ |
      | RINGAN       |
      | SEDANG       |
      | LEBAT        |
      | SANGAT LEBAT |

  - `weather` (Array)

    Array of weather value obtained from all observatory stations. If there are
    no data in the current time range, the value would be an empty array. Below
    is the list of all possible values:

    | Weather |
    | ------- |
    | CERAH   |
    | BERAWAN |
    | MENDUNG |
    | HUJAN   |
    | BADAI   |

- `visual` (Object)

  Visual information data in the current observation time range. It is an object
  containing the following fields:

  - `visibility` (Array)

    Possible visibility values given by observers from all observatory stations
    within certain time range. Below is the list of all possible values:

    | Visibility |
    | ---------- |
    | TAMPAK     |
    | KABUT 01   |
    | KABUT 02   |
    | KABUT 03   |

  - `smoke` (Object | null)

    Observed volcano smoke information with the highest height value. It is an
    object containing the following fields:

    - `color` (String)

      Smoke color. Possible values are:

      | Color  |
      | ------ |
      | PUTIH  |
      | COKLAT |
      | KELABU |
      | HITAM  |

    - `direction` (String)

      Smoke direction. Possible values are:

      | Direction  |
      | ---------- |
      | TIMUR      |
      | TENGGARA   |
      | SELATAN    |
      | BARAT DAYA |
      | BARAT      |
      | BARAT LAUT |
      | UTARA      |
      | TIMUR LAUT |

    - `intensity` (String)

      Smoke intensity. Possible values are:

      | Intensity |
      | --------- |
      | TIPIS     |
      | SEDANG    |
      | TEBAL     |

    - `pressure` (String)

      Smoke pressure. Possible values are:

      | Pressure |
      | -------- |
      | LEMAH    |
      | SEDANG   |
      | KUAT     |

    - `height` (Number)

      Maximum smoke height in meter.

    - `occurredAt` (Number)

      Timestamp when the observation took place, e.g. `2022-04-10 05:55:00`.

  - `ap` (Object | null)

    Observed Awan Panas (AP) event information. If no events in the current
    observation time period, it would be null. If there are any events, it would
    an object containing the following fields:

    - `max_distance` (Number)

      The maximum distance of AP event in meter.

    - `direction` (String)

      The direction of AP event whose distance is maximum. Possible values are:

      |     Value      |  Description   |
      | -------------- | -------------- |
      | Tidak Teramati | Tidak Teramati |
      | Apu            | Kali Apu       |
      | Batang         | Kali Batang    |
      | Bebeng         | Kali Bebeng    |
      | Bedog          | Kali Bedog     |
      | Boyong         | Kali Boyong    |
      | Gendol         | Kali Gendol    |
      | Krasak         | Kali Krasak    |
      | Kuning         | Kali Kuning    |
      | Lamat          | Kali Lamat     |
      | Opak           | Kali Opak      |
      | Sat/Putih      | Kali Sat/Putih |
      | Senowo1        | Kali Senowo1   |
      | Senowo2        | Kali Senowo2   |
      | Senowo3        | Kali Senowo3   |
      | Trising        | Kali Trising   |
      | Woro           | Kali Woro      |
      | TIMUR          | TIMUR          |
      | TENGGARA       | TENGGARA       |
      | SELATAN        | SELATAN        |
      | BARAT DAYA     | BARAT DAYA     |
      | BARAT          | BARAT          |
      | BARAT LAUT     | BARAT LAUT     |
      | UTARA          | UTARA          |
      | TIMUR LAUT     | TIMUR LAUT     |

    - `count` (Number)

      The number of AP events occurred within observation period.

  - `rf` (Object | null)

    Observed Rockfall (Guguran Lava Pijar) event information. If no event
    observed within time interval, the value would be null. If there are any
    events, the value would be an object with the following fields:

    - `max_distance` (Number)

      The maximum distance of RF event in meter.

    - `direction` (String)

      The direction of RF event whose distance is maximum. Possible values are
      similar with AP directions.

    - `count` (Number)

      The number of RF events occurred within observation period.

- `seismicity` (Array)

  Seismicity information observed within current time range. It is an array
  containing seismicity object. The seismicity object contains the following
  fields:

  - `code` (String)

    Earthquake event code. Possible values are:

    | Event Code |    Description     |
    | ---------- | ------------------ |
    | VTA        | Vulkanik Dalam     |
    | VTB        | Vulkanik Dangkal   |
    | MP         | Hybrid/Fase Banyak |
    | LF         | Low Frekuensi      |
    | ROCKFALL   | Guguran            |
    | GASBURST   | Hembusan           |
    | TECT       | Tektonik Jauh      |
    | TECLOC     | Tektonik Lokal     |
    | EXPLOSION  | Letusan            |
    | AWANPANAS  | Awan Panas         |
    | TREMOR     | Tremor Harmonik    |
    | ANTHROP    | Anthropogenic      |
    | SOUND      | Suara              |
    | TELE       | Teleseismik        |
    | TPHASE     | T-Phase            |
    | UNKNOWN    | Unknown            |
    | LAHAR      | Lahar              |

  - `name` (String)

    Event name in Indonesian, e.g. Guguran, Low Frekuensi, etc.

  - `count` (Number)

    Event count within current time range.

  - `amplitude` (Number | Object | null)

    Event amplitude in mm if there is only one event, or an object containing
    minimum (`min`) and maximum (`max`) of amplitudes in mm if there are
    multiple events. If there are no data in current time range, the value would
    be `null`.

  - `duration` (Number | Object | null)

    Event duration is seconds if there is only one event, or an object
    containing minimum and maximum of duration in seconds if there are multiple
    events. If there are no data in the current time range, the value would be
    `null`.

  Note that seismicity array will only contain observed events within current
  period or time interval.

- `observer` (Array)

  An array containing all observers information. If there aren't any observer,
  it will contain empty array.
  
  The array contains an object with the following fields:

  - `gid` (String)

    Global unique identifier of current observer, e.g. `80`, `78`.

  - `nip` (String)

    NIP (Nomor Induk Pegawai) number. For current version, we restrict observer
    list for PNS only. In rare case, if NIP is not inputted yet by our
    administrator, it will contain empty string.

  - `name` (String)

    Name of current observer, e.g. `Suratman`.

- `photo` (Object | null)

  Photo visual of the volcano. If there are no data in the current time range,
  the value would be `null`.

  If any, the object will contains the following fields:

  - `location` (String)

    The location where the photo was taken, e.g. `Kaliurang`, `Babadan`.

  - `url` (String)

    The URL of the photo image.

  - `takenAt` (String)

    Timestamp when the photo was captured, e.g. `2022-04-10 05:24:00`.

- `createdAt` (String)

  Timestamp when the report was created, e.g. `2022-04-10 07:52:03`.

- `shake` (Array)

  Array of integer containing the value of Modified Mercalli Intensity (MMI)
  scale that was felt by the observers. The scale value would be within 1 to 12.
  If there are no data in the current time range, the value would be an empty
  array.

  Example: `[4, 3, 6]`

- `others` (Array)

  Array containing object of other events that may count as significant. If
  there aren't no events, it will be an empty array. If any, it each object
  contains the following fields:

  - `description` (String)

    The description of event.

  - `occurredAt` (String)

    Timestamp when the event occurred, e.g. `2022-04-10 09:50:00`.

- `activityLevel` (Object)

  Current activity level of the Merapi. The object contains the following fields:

  - `level` (Number)

    Numeric value indicating the level of activity. Possible values are: 1, 2,
    3, 4.

  - `status` (String)

    The current status of activity level in capital string. Possible values are:
    `NORMAL`, `WASPADA`, `SIAGA`, `AWAS`.

  - `date` (String)

    Date when the current level was declared in YYYY-mm-dd format.

  See below table for detailed associated level and status relations:

    | Level | Level Roman | Status  | Description |
    | ----- | ----------- | ------- | ----------- |
    | 1     | I           | NORMAL  | Normal      |
    | 2     | II          | WASPADA | Waspada     |
    | 3     | III         | SIAGA   | Siaga       |
    | 4     | IV          | AWAS    | Awas        |

- `recommendation` (String)

  A string containing all recommendations by authority regarding the current
  activity level.

## Error Handling

For certain cases, the request to the backend may fails. Several factors causing
these are:

- Incorrect parameters configuration from the client.

  If client incorectly set the parameter configuration the backend could not
  process the request. Verify again if your request parameters are correct.

  The backend may send 400 HTTP error status if it could not process the
  request. For example:

      GET /api/public/v1/magmavar?date=21/11/16

  Example response:

  ```json
  {"message":"Invalid date string."}
  ```

- Connection problem from the client to the backend server.

  It may due to internet connection problem. Check again that your internet
  connection is working.

- The backend server is down.

  It is a rare case where our server is down due to technical problem. You can
  contact the project maintainers if you experience with this problem.

- etc.

## Deprecations

Whenever possible, the API aims to preserve backwards compatibility for its
users. Apps you write on top of the API now should continue to work
indefinitely. However, there are a few rare cases where breaking changes are
required in the future.

If a breaking change is required, we will communicate early, and through a
variety of channels to help the developers get through the change. Primarily, we
use this documentation to give an early update if there are changes in the API.

## Support and Feedback

If you have any question about or experiencing a problem with this API, you can
raise an issue to our project repository on
[GitLab](https://gitlab.com/bpptkg/bpptkg-backend) or contact our project
maintainers directly.

Copyright (c) 2020-present BPPTKG

## Changelog

- 2023-04-01

  Added Awan Panas and Rockfall observation events in the visual data.

  - Added `ap` and `rf` fields to `visual` data.
