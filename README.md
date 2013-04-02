# API

Reverse engineered API specification for 9292.nl. Only to be used in educational purposes.

## Host

- https://api.9292.nl

## Params

- lat (Double) Latitude
- long (Double) Longitude
- station (String) An arbitrary station name
- location (String) An location
- station_id (String) Station id given by the location hash
- date (String) In yyyy-MM-dd'T'HHmm
- search_type (String) Should :date be the departure time (vertrek) or arrival (aankomst)?
- by_train (Boolean)
- by_ferry (Boolean)
- by_tram (Boolean)
- by_bus (Boolean)
- by_subway (Boolean)
- interchange_time (Integer) (1) Add 5 min extra (0) between each change?
- sequence (Integer) (1) Unknown
- before (Integer) (1) Unknown
- after (Integer) (5) Unknown
- via (String) See :station_id
- from (String) See :station_id
- to (String) See :station_id
- lang
  - nl-NL
  - en-GB

## Requests

### Search stations by name

```
GET /0.1/locations?
  lang=:lang&
  type=station,stop&
  q=:station
```

``` javascript
{
  "locations": [
    {
      "id": "utrecht/bushalte-vasco-da-gamalaan-7-14",
      "type": "stop",
      "stopType": "Bus stop",
      "name": "Vasco Da Gamalaan (7/14)",
      "place": {
        "name": "Utrecht",
        "regionCode": "UT",
        "regionName": "Utrecht",
        "showRegion": false,
        "countryCode": "NL",
        "countryName": "The Netherlands",
        "showCountry": false
      },
      "latLong": {
        "lat": 52.066465,
        "long": 5.096992
      },
      "urls": {
        "nl-NL": "/utrecht/bushalte-vasco-da-gamalaan-7-14",
        "en-GB": "/en/utrecht/bushalte-vasco-da-gamalaan-7-14"
      }
    }
  ]
}
```

### Search locations by name

```
GET /0.1/locations?
  lang=:lang&
  q=:location
```

``` javascript
{
  "locations": [
    {
      "id": "utrecht/bushalte-azielaan",
      "type": "stop",
      "stopType": "Bus stop",
      "name": "Azielaan",
      "place": {
        "name": "Utrecht",
        "regionCode": "UT",
        "regionName": "Utrecht",
        "showRegion": false,
        "countryCode": "NL",
        "countryName": "The Netherlands",
        "showCountry": false
      },
      "latLong": {
        "lat": 52.064313,
        "long": 5.099047
      },
      "urls": {
        "nl-NL": "/utrecht/bushalte-azielaan",
        "en-GB": "/en/utrecht/bushalte-azielaan"
      }
    }
  ]
}
```

### Search stations by longitude and latitude

```
GET /0.1/locations?
  lang=:lang&
  type=station,stop&
  latlong=:lat,:long&
  includestation=true
```

``` javascript
{
  "locations": [
    {
      "id": "utrecht/bushalte-vasco-da-gamalaan-7-14",
      "type": "stop",
      "stopType": "Bus stop",
      "name": "Vasco Da Gamalaan (7/14)",
      "place": {
        "name": "Utrecht",
        "regionCode": "UT",
        "regionName": "Utrecht",
        "showRegion": false,
        "countryCode": "NL",
        "countryName": "The Netherlands",
        "showCountry": false
      },
      "latLong": {
        "lat": 52.066465,
        "long": 5.096992
      },
      "urls": {
        "nl-NL": "/utrecht/bushalte-vasco-da-gamalaan-7-14",
        "en-GB": "/en/utrecht/bushalte-vasco-da-gamalaan-7-14"
      }
    }
  ]
}
```

### List departure times for a station

```
GET /0.1/locations/:station_id/departure-times?
  lang=:lang
```

``` javascript
{
  "location": {
    "id": "utrecht/bushalte-vasco-da-gamalaan-7-14",
    "type": "stop",
    "stopType": "Bus stop",
    "name": "Vasco Da Gamalaan (7/14)",
    "place": {
      "name": "Utrecht",
      "regionCode": "UT",
      "regionName": "Utrecht",
      "showRegion": false,
      "countryCode": "NL",
      "countryName": "The Netherlands",
      "showCountry": false
    },
    "latLong": {
      "lat": 52.066465,
      "long": 5.096992
    },
    "urls": {
      "nl-NL": "/utrecht/bushalte-vasco-da-gamalaan-7-14",
      "en-GB": "/en/utrecht/bushalte-vasco-da-gamalaan-7-14"
    }
  },
  "tabs": [
    {
      "id": "bus",
      "name": "Bus",
      "locations": [
        {
          "id": "utrecht/bushalte-vasco-da-gamalaan-7-14",
          "type": "stop",
          "stopType": "Bushalte",
          "name": "Vasco Da Gamalaan (7/14)",
          "place": {
            "name": "Utrecht",
            "regionCode": "UT",
            "regionName": "Utrecht",
            "showRegion": false,
            "countryCode": "NL",
            "countryName": "Nederland",
            "showCountry": false
          },
          "latLong": {
            "lat": 52.066465,
            "long": 5.096992
          },
          "urls": {
            "nl-NL": "/utrecht/bushalte-vasco-da-gamalaan-7-14",
            "en-GB": "/en/utrecht/bushalte-vasco-da-gamalaan-7-14"
          }
        }
      ],
      "departures": [
        {
          "time": "15:58",
          "destinationName": "Overvecht Noord",
          "viaNames": null,
          "mode": {
            "type": "bus",
            "name": "Citybus"
          },
          "operatorName": "GVU",
          "service": "7",
          "platform": null,
          "platformChanged": false,
          "remark": null,
          "realtimeState": "ontime",
          "realtimeText": null
        }
      ]
    }
  ]
}
```

### Get closest location

```
GET /0.1/locations?
  lang=:lang&
  latlong=:lat,:long&
  type=address&
  rows=1
```

``` javascript
{
  "locations": [
    {
      "id": "utrecht/columbuslaan-355",
      "type": "address",
      "name": "Columbuslaan",
      "houseNr": "355",
      "place": {
        "name": "Utrecht",
        "regionCode": "UT",
        "regionName": "Utrecht",
        "showRegion": false,
        "countryCode": "NL",
        "countryName": "The Netherlands",
        "showCountry": false
      },
      "latLong": {
        "lat": 52.066483,
        "long": 5.097021
      }
    }
  ]
}
```

### Get journeys

```
GET /0.1/journeys?
  lang=:lang&
  dateTime=:date&
  to=:station_id&
  from=:station_id&
  searchType=:search_type&
  sequence=1&
  interchangeTime=:interchange_time&
  before=:before&
  after=:after&
  byTrain=:by_tram&
  byFerry=:by_ferry&
  byTram=:by_tram&
  byBus=:by_bus&
  bySubway=:by_subway
```

``` javascript
{
  "journeys": [
    {
      "id": "fromRef=utrecht/tramhalte-tram-centraal-station&toRef=utrecht/bushalte-vasco-da-gamalaan-7-14&searchType=arrival&dateTime=2013-03-30T17:52&interchangeTime=extra&sequence=1&modes=train:false,bus:true,subway:false,tram:true,ferry:false",
      "ludMessages": [],
      "fasterJourneyId": null,
      "departure": "2013-03-30T17:38",
      "arrival": "2013-03-30T17:52",
      "numberOfChanges": 0,
      "legs": [
        {
          "type": "scheduled",
          "mode": {
            "type": "tram",
            "name": "Sneltram"
          },
          "destination": "IJsselstein",
          "operator": {
            "type": "connexxion",
            "name": "Connexxion"
          },
          "service": "ST",
          "attributes": [],
          "disturbancePlannerIds": [],
          "serviceMessageIds": [],
          "stops": [
            {
              "arrival": null,
              "departure": "2013-03-30T17:38",
              "platform": null,
              "location": {
                "id": "utrecht/tramhalte-tram-centraal-station",
                "type": "stop",
                "stopType": "Tram stop",
                "name": "Tram Centraal Station",
                "place": {
                  "name": "Utrecht",
                  "regionCode": "UT",
                  "regionName": "Utrecht",
                  "showRegion": false,
                  "countryCode": "NL",
                  "countryName": "The Netherlands",
                  "showCountry": false
                },
                "latLong": {
                  "lat": 52.091727,
                  "long": 5.110252
                },
                "urls": {
                  "nl-NL": "/utrecht/tramhalte-tram-centraal-station",
                  "en-GB": "/en/utrecht/tramhalte-tram-centraal-station"
                }
              },
              "fallbackName": null
            }
          ]
        },
        {
          "type": "continuous",
          "duration": "00:06",
          "mode": {
            "type": "walk",
            "name": "Lopen van/naar bestemming"
          },
          "stops": [
            {
              "arrival": null,
              "departure": null,
              "platform": null,
              "location": {
                "id": "utrecht/bus-tramhalte-vasco-da-gamalaan-sneltram",
                "type": "stop",
                "stopType": "Tram stop",
                "name": "Vasco Da Gamalaan (Sneltram)",
                "place": {
                  "name": "Utrecht",
                  "regionCode": "UT",
                  "regionName": "Utrecht",
                  "showRegion": false,
                  "countryCode": "NL",
                  "countryName": "The Netherlands",
                  "showCountry": false
                },
                "latLong": {
                  "lat": 52.068151,
                  "long": 5.102494
                },
                "urls": {
                  "nl-NL": "/utrecht/bus-tramhalte-vasco-da-gamalaan-sneltram",
                  "en-GB": "/en/utrecht/bus-tramhalte-vasco-da-gamalaan-sneltram"
                }
              },
              "fallbackName": null
            }
          ]
        }
      ],
      "fareInfo": {
        "complete": true,
        "fullPriceCents": 132,
        "reducedPriceCents": 132,
        "legs": [
          {
            "from": {
              "id": "utrecht/tramhalte-tram-centraal-station",
              "type": "stop",
              "stopType": "Tram stop",
              "name": "Tram Centraal Station",
              "place": {
                "name": "Utrecht",
                "regionCode": "UT",
                "regionName": "Utrecht",
                "showRegion": false,
                "countryCode": "NL",
                "countryName": "The Netherlands",
                "showCountry": false
              },
              "latLong": {
                "lat": 52.091727,
                "long": 5.110252
              },
              "urls": {
                "nl-NL": "/utrecht/tramhalte-tram-centraal-station",
                "en-GB": "/en/utrecht/tramhalte-tram-centraal-station"
              }
            },
            "to": {
              "id": "utrecht/bus-tramhalte-vasco-da-gamalaan-sneltram",
              "type": "stop",
              "stopType": "Tram stop",
              "name": "Vasco Da Gamalaan (Sneltram)",
              "place": {
                "name": "Utrecht",
                "regionCode": "UT",
                "regionName": "Utrecht",
                "showRegion": false,
                "countryCode": "NL",
                "countryName": "The Netherlands",
                "showCountry": false
              },
              "latLong": {
                "lat": 52.068151,
                "long": 5.102494
              },
              "urls": {
                "nl-NL": "/utrecht/bus-tramhalte-vasco-da-gamalaan-sneltram",
                "en-GB": "/en/utrecht/bus-tramhalte-vasco-da-gamalaan-sneltram"
              }
            },
            "locationsString": "Utrecht",
            "modeTypeString": "Tram",
            "operatorString": "Connexxion",
            "fares": [
              {
                "class": "none",
                "reduced": false,
                "eurocents": 132
              },
              {
                "class": "none",
                "reduced": true,
                "eurocents": 87
              }
            ]
          }
        ]
      }
    }
  ],
  "earlier": "/0.1/journeys?lang=en-GB&from=utrecht%2Ftramhalte-tram-centraal-station&to=utrecht%2Fbushalte-vasco-da-gamalaan-7-14&searchType=arrival&dateTime=2013-03-30T1752&sequence=1&byTrain=false&byBus=true&bySubway=false&byTram=true&byFerry=false&interchangeTime=extra&after=-1",
  "later": "/0.1/journeys?lang=en-GB&from=utrecht%2Ftramhalte-tram-centraal-station&to=utrecht%2Fbushalte-vasco-da-gamalaan-7-14&searchType=arrival&dateTime=2013-03-30T1837&sequence=1&byTrain=false&byBus=true&bySubway=false&byTram=true&byFerry=false&interchangeTime=extra&before=-1",
  "disturbances": [],
  "serviceMessages": [],
  "nearbyAddresses": []
}
```