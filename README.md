# SWAPI Tutorial

The Star Wars API (SWAPI) allows users to access a multitude of data about Star
Wars including People, Films, Planets, and more! This tutorial will walk you
through how to search for a movie that features Luke Skywalker.

## The Basics

The base URL for searching SWAPI is `https://swapi.dev/api/`. This should be
added to the beginning of any endpoints you are accessing.

Since SWAPI is an open API, no authentication is needed to access the data.
Without further ado, we can get straight to our search for Luke Skywalker!

## People Endpoint

This API allows us to search for people in a few ways:

- `/people/` -- Retrieves all people resources in the database.
- `/people/:id/` -- Gets data on a specific person.
- `/people/schema/` -- Retrieves the schema for the people endpoint in JSON
  format.

If you're interested to see what information we will be looking at you can make
a request for the schema, but for our purposes the second call, `/people/:id/`
seems like what we need. However, we don't know what ID Luke Skywalker is
located at.

To find out, we can access the `/people/` endpoint and skim the results for Luke
Skywalker, but SWAPI generously provides a much easier way to find the data we
are seeking.

We can perform a curl request that looks like this:

```
curl "https://swapi.dev/api/people/?search=luke+skywalker"
```

We are accessing the `search` parameter which filters the `/people/` endpoint
based on the terms we provide, in this case `luke+skywalker`.

The result looks like this:

```json
{
  "count": 1,
  "next": null,
  "previous": null,
  "results": [
    {
      "name": "Luke Skywalker",
      "height": "172",
      "mass": "77",
      "hair_color": "blond",
      "skin_color": "fair",
      "eye_color": "blue",
      "birth_year": "19BBY",
      "gender": "male",
      "homeworld": "http://swapi.dev/api/planets/1/",
      "films": [
        "http://swapi.dev/api/films/1/",
        "http://swapi.dev/api/films/2/",
        "http://swapi.dev/api/films/3/",
        "http://swapi.dev/api/films/6/"
      ],
      "species": [],
      "vehicles": [
        "http://swapi.dev/api/vehicles/14/",
        "http://swapi.dev/api/vehicles/30/"
      ],
      "starships": [
        "http://swapi.dev/api/starships/12/",
        "http://swapi.dev/api/starships/22/"
      ],
      "created": "2014-12-09T13:50:51.644000Z",
      "edited": "2014-12-20T21:17:56.891000Z",
      "url": "http://swapi.dev/api/people/1/"
    }
  ]
}
```

We can see that there is an array of films provided, but we still don't know
which films Luke Skywalker is in without making further calls to the films
endpoint, so we will take a look at that next.

## Films Endpoint

The films array retrieved from the Luke Skywalker call looked like this:

```json
{
  ...
  "films": [
        "http://swapi.dev/api/films/1/",
        "http://swapi.dev/api/films/2/",
        "http://swapi.dev/api/films/3/",
        "http://swapi.dev/api/films/6/"
    ],
    ...
}
```

Since the API calls we need to make have been provided in the response, our job
from here is quite simple. To provide a quick overview, the films endpoints are
almost identical to the people endpoints:

- `/films/` -- Retrieves all film resources in the database.
- `/films/:id/` -- Gets data on a specific film.
- `/films/schema/` -- Retrieves the schema for the films endpoint in JSON
  format.

To access the films Luke Skywalker has been in we can access `/films/1/`,
`/films/2/`, `/films/3/`, and `/films/6/`.

Here's a sample of the result of a call to `/films/1`:

```json
{
  "title": "A New Hope",
  "episode_id": 4,
  "opening_crawl": "It is a period of civil war.Rebel spaceships, striking from a hidden base, have won their first victory against the evil Galactic Empire. During the battle, Rebel spies managed to steal secret plans to the Empire's ultimate weapon, the DEATH STAR, an armored space station with enough power to destroy an entire planet.Pursued by the Empire's sinister agents, Princess Leia races home aboard her starship, custodian of the stolen plans that can save her people and restore freedom to the galaxy....",
  "director": "George Lucas",
  "producer": "Gary Kurtz, Rick McCallum",
  "release_date": "1977-05-25",
  "characters": [
    "http://swapi.dev/api/people/1/",
    "http://swapi.dev/api/people/2/",
    "http://swapi.dev/api/people/3/",
    "http://swapi.dev/api/people/4/",
    "http://swapi.dev/api/people/5/",
    "http://swapi.dev/api/people/6/",
    "http://swapi.dev/api/people/7/",
    "http://swapi.dev/api/people/8/",
    "http://swapi.dev/api/people/9/",
    "http://swapi.dev/api/people/10/",
    "http://swapi.dev/api/people/12/",
    "http://swapi.dev/api/people/13/",
    "http://swapi.dev/api/people/14/",
    "http://swapi.dev/api/people/15/",
    "http://swapi.dev/api/people/16/",
    "http://swapi.dev/api/people/18/",
    "http://swapi.dev/api/people/19/",
    "http://swapi.dev/api/people/81/"
  ],
  "planets": [
    "http://swapi.dev/api/planets/1/",
    "http://swapi.dev/api/planets/2/",
    "http://swapi.dev/api/planets/3/"
  ],
  "starships": [
    "http://swapi.dev/api/starships/2/",
    "http://swapi.dev/api/starships/3/",
    "http://swapi.dev/api/starships/5/",
    "http://swapi.dev/api/starships/9/",
    "http://swapi.dev/api/starships/10/",
    "http://swapi.dev/api/starships/11/",
    "http://swapi.dev/api/starships/12/",
    "http://swapi.dev/api/starships/13/"
  ],
  "vehicles": [
    "http://swapi.dev/api/vehicles/4/",
    "http://swapi.dev/api/vehicles/6/",
    "http://swapi.dev/api/vehicles/7/",
    "http://swapi.dev/api/vehicles/8/"
  ],
  "species": [
    "http://swapi.dev/api/species/1/",
    "http://swapi.dev/api/species/2/",
    "http://swapi.dev/api/species/3/",
    "http://swapi.dev/api/species/4/",
    "http://swapi.dev/api/species/5/"
  ],
  "created": "2014-12-10T14:23:31.880000Z",
  "edited": "2014-12-20T19:49:45.256000Z",
  "url": "http://swapi.dev/api/films/1/"
}
```

From here we can access plenty of data about other characters, planets, and
starships featured in the film.

## Conclusion

This tutorial has provided a walkthrough of accessing the films that feature
Luke Skywalker in the Star Wars API.

Please refer to the [official documentation](https://swapi.dev/documentation)
for further information on other endpoints and data you can access. You can also
find a number of language specific SDK's here to easily import this API into
your projects.
