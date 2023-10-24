- I will be getting the information from Kiu
- I have to implement it with an existing project of ReactJS 

Looking for inspiration,  I found this: [SeatPicker (forked) - CodeSandbox](https://codesandbox.io/s/seatpicker-forked-uwp5g)

It's sort of how I want the seat selection to work, just in a more refined way

## Kiu response for seat availability

**Can be seen [HERE](https://kiuws-docs-agencies.kiusys.net/#6a7a1a71-a63a-4739-bafd-29f4406ca97e)**

Here's an answer about the structure provided by chatGPT:

[[chatGPT answer about Kiu Seat availability]]

### Extra notes

- On the `<column>` tag, I think that tha "position" attribute means the relative position of the column on the plane, where `"W"` means a column located on the wing, `"9"` a column located between two columns, and  `"A"` means that the seat is adjacent to a hallway

> Example: `<Columns Position="W">A</Columns>`

- On the `<Location>` tag, there's another one named `<Status>`, I think this one can have three values: `"F"` for "Free", `"R"` for "Reserved", and `"O"` for ocuppied

## Parsed response currently present in the API

We currently parse the response as follows (according to chatGPT): 

```json
{
  "flightNumber": "ABC123",
  "departureInformation": {
    "dateTime": "l",
    "locationCode": "DEP123",
    "airportName": "Departure Airport",
    "cityName": "Departure City"
  },
  "arrivalInformation": {
    "dateTime": "l",
    "locationCode": "ARR456",
    "airportName": "Arrival Airport",
    "cityName": "Arrival City"
  },
  "equipmentInformation": {
    "code": "EQUIP789",
    "description": "Equipment Description"
  },
  "cabin": [
    {
      "firstRow": 1,
      "lastRow": 10,
      "cabinClass": {
        "code": "CAB001",
        "definition": "Cabin Class Definition"
      },
      "columns": [
        {
          "position": "A",
          "codeType": "Column Description A"
        },
        {
          "position": "B",
          "codeType": "Column Description B"
        }
      ],
      "rows": [
        {
          "rowNumber": 1,
          "seats": [
            {
              "column": "A",
              "seatNumber": "1A",
              "occupied": false,
              "characteristics": {
                "code": "I",
                "description": ""
              }
            },
            {
              "column": "B",
              "seatNumber": "",
              "occupied": true,
              "characteristics": {
                "code": "",
                "description":""
              }
            }
          ]
        }
      ]
    }
  ]
}
```

the information that we are going to be used is under `cabin.rows.seats`, since this is the part that describes the position of the seats in the plane 

## Destructuring of the problem

1.  [x] Display a Single Seat
2.  [x] Display all the seats from a single row
3.  [x] Display all the seats from every row
4.  [ ] Sort and Label the Rows and Columns
5.  [ ] Display different color depending on the status and class of the seat
6.  [ ] Make them selectable and save the column and row of the seat (i.e. {row: 5, column: B})

**DATASET:** ![[seatMap.json]]
- LAST NAME has to be in uppercase


## Questions

- is it permitted to not select all available seats? for example: if there are 4 passengers, select only 2 seats
- should I include seat price tax when showing to user?
- standard seats are not selectable or free?


## New Kiu endpoints

- AirOfferList 
	- DateTime
	- FlightNumber
	- off point
	- on point

- SeatAvailabilityV2
	- PNR
	- Date
	- FlightNumber
	- off point
	- on point

- ModifyBooking
	- PNR
	- seats to select

## Database

> NOTE: I modified the testing database to have the seat ancillary

