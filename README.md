# VRP [![Build Status](https://travis-ci.org/notdodo/VRP-tabu.svg?branch=master)](https://travis-ci.org/notdodo/VRP-tabu)
This repo contains the project of "Metodi ed Algoritmi di Ottimizzazione per il Problem Solving": a parallel algorithm for [VRP](https://en.wikipedia.org/wiki/Vehicle_routing_problem) with [tabu search](https://en.wikipedia.org/wiki/Tabu_search) heuristic.
This program reads data from a JSON file which holds all informations about customers, vehicles, depot and requests.

This simple example shows a configuration of 3 customers to serve with 2 vehicles with max capacity of 400 and max work time of 350. Each customer has a name, a position, an amount of resources requested and an optional service time. In order to create the best routes it's necessary to know the cost of each travel from each customers (in this case the distance is the geometric distance).
```json
{
  "vertices": [
    {
      "name": "v0",
      "x": 0,
      "y": 0
    },
    {
      "name": "v1",
      "x": -17,
      "y": 181,
      "request": 33,
      "time": 16
    },
    {
      "name": "v2",
      "x": -237,
      "y": -13,
      "request": 7,
      "time": 11
    },
    {
      "name": "v3",
      "x": -170,
      "y": -193,
      "request": 15,
      "time": 9
    }
  ],
  "vehicles": 2,
  "capacity": 400,
  "worktime": 350,
  "costs": [
    [
      {
        "from": 0,
        "to": 1,
        "value": 181
      },
      {
        "from": 0,
        "to": 2,
        "value": 237
      },
      {
        "from": 0,
        "to": 3,
        "value": 257
      }
    ],
    [
      {
        "from": 1,
        "to": 0,
        "value": 181
      },
      {
        "from": 1,
        "to": 2,
        "value": 293
      },
      {
        "from": 1,
        "to": 3,
        "value": 404
      }
    ],
    [
      {
        "from": 2,
        "to": 0,
        "value": 237
      },
      {
        "from": 2,
        "to": 1,
        "value": 293
      },
      {
        "from": 2,
        "to": 3,
        "value": 192
      }
    ],
    [
      {
        "from": 3,
        "to": 0,
        "value": 257
      },
      {
        "from": 3,
        "to": 1,
        "value": 404
      },
      {
        "from": 3,
        "to": 2,
        "value": 192
      }
    ]
  ]
}
```
The position of each customer matches a coordinate in the Cartesian Plane (with 4 quadrants).

After the execution of the program the output file should be like this:
```json
{
    "vertices": [
        {
            "name": "v0",
            "x": 0,
            "y": 0
        },
        {
            "name": "v1",
            "x": -17,
            "y": 181,
            "request": 33,
            "time": 16
        },
        {
            "name": "v2",
            "x": -237,
            "y": -13,
            "request": 7,
            "time": 11
        },
    [....]
      [
            {
                "from": 4,
                "to": 2,
                "value": 408
            },
            {
                "from": 4,
                "to": 3,
                "value": 427
            }
        ]
    ],
    "routes": [
        [
            "v0",
            "v1",
            "v2",
            "v3",
            "v0"
        ],
        [
            "v0",
            "v4",
            "v0"
        ]
    ],
    "costs": [
        923,
        356
    ]
}
```
The program appended two more attribute which represent the final routes with relative costs.
The first route costs '923' and is:
`v0 -> v1 -> v2 -> v3 -> v0`.

The second route costs '356' and the path is:
`v0 -> v4 -> v0`

## Web-UI
Creating files as the example above is something long and tedious, expecially for complex initial configurations.
The [Web-UI](vrp-init/), created in HTML5, CSS3 and JavaScript, allows easily generation of JSON input file creating various clients with a click. User can set all other settings without writing a single line of JSON.

![Example with customers](https://raw.githubusercontent.com/edoz90/VRP-tabu/master/screenshot/customers.png "Example")

The application could be run in a web server or simply opening the file `index.html`.

After creating and executing the JSON file through the VRP program the Web-UI can read the output file to display costs and routes.

![Example of routes](https://raw.githubusercontent.com/edoz90/VRP-tabu/master/screenshot/routes.png "Routes and costs")

## Run

Compile with: `make`

Usage: `./VRP [-v] data.json`

## Documentation
Run `doxygen` in root folder and the documentation will be generated in `doc/` folder
