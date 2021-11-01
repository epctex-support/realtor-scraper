# Actor - Realtor Scraper

## Realtor scraper

Since Realtor doesn't provide an API, this actor should help you to retrieve data from it.

The Realtor data scraper supports the following features:

-   Scrape property details - You can scrape attributes like property images, price, features, neighborhood, nearby schools and many more. You can find details below.

-   Scrape sold properties - You can scrape sold properties through a search list.

-   Scrape for sale properties - If you are looking for a property which is for sale, you can directly target them.

-   Scrape rental properties - Rental properties can be directly targeted.

-   Scrape by keyword - You can use location-wise keywords to search specific search lists. Also you can directly point out rental, for sale or sold properties on this feature.

-   Scrape properties by filter - Auto detection of URLs helps you to directly copy/paste the URLs into the scraper to apply any filtering you like.

#### Realtor specific

Don't worry when you get little bit different properties than you saw in browser page. Realtor is ordering properties differently for each user.

## Bugs, fixes, updates and changelog

This scraper is under active development. If you have any feature requests you can create an issue from [here](https://github.com/tugkan/realtor-scraper/issues).

### Incoming Changes

-   Fetching property historical data
-   Fetch Realtor agents

## Setup & Usage

You can see how this actor works in this video:

### Start URLs

[![Apify - Realtor Scraper - Using Start URLs](https://img.youtube.com/vi/BV5IjXYtFlw/0.jpg)](https://www.youtube.com/watch?v=BV5IjXYtFlw)

You can check the output of this video [here](https://api.apify.com/v2/datasets/aPEEmNEH4vJzQaxHe/items?clean=true&format=json).

### Search

[![Apify - Realtor Scraper - Using Search & Mode ](https://img.youtube.com/vi/s_0lgZD7m7g/0.jpg)](https://www.youtube.com/watch?v=s_0lgZD7m7g)

You can check the output of this video [here](https://api.apify.com/v2/datasets/FW4mdbh8UmOWzhswP/items?clean=true&format=json).

## Input Parameters

The input of this scraper should be JSON containing the list of pages on Realtor that should be visited. Required fields are:

| Field                | Type    | Description                                                                                                                                                                                               |
| -------------------- | ------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| startUrls            | Array   | (optional) List of Realtor URLs. You should only provide property detail or search URLs                                                                                                                   |
| maxItems             | Integer | (optional) You can limit scraped products. This should be useful when you search through the big subcategories.                                                                                           |
| endPage              | Integer | (optional) Final number of page that you want to scrape. Default is `Infinite`.                                                                                                                           |
| search               | String  | (optional) Keyword that can be searched in Realtor search engine. When it is present, `mode` must be used as well.                                                                                        |
| mode                 | String  | (optional) Mode of the actor. It gets the keyword from `search` parameter and initiate the search according to the mode. Can be `BUY`, `RENT` or `SOLD`. When present, `search` must be provided as well. |
| extendOutputFunction | String  | (optional) Function that takes a JQuery handle ($) as argument and returns object with data                                                                                                               |
| proxy                | Object  | Proxy configuration                                                                                                                                                                                       |

This solution requires the use of **Proxy servers**, either your own proxy servers or you can use [Apify Proxy](https://www.apify.com/docs/proxy).

##### Tip

When you want to have a filtering over a search URL; go to Realtor, create filters over the serach list and copy and paste the link as one of the **startUrl**.

If you would like to scrape only the first page of a search list or search list, then put the link for the page and have the `endPage` as 1.

With the last approach that explained above you can also fetch any interval of pages. If you provide the 5th page of a search list and define the `endPage` parameter as 6 then you'll have the 5th and 6th pages only.

### Compute Unit Consumption

The actor optimized to run blazing fast and scrape many as properties as possible. Therefore, it forefronts all property detail requests. If actor doesn't block very often it'll scrape 50 properties in 2 minutes with ~0.05-0.07 compute units.

### Realtor Scraper Input example

```json
{
    "startUrls": [
        "https://www.realtor.com/realestateandhomes-detail/9325-W-Desert-Inn-Rd-Apt-116_Las-Vegas_NV_89117_M25429-00790",
        "https://www.realtor.com/realestateandhomes-detail/6655-S-Fort-Apache-Rd_Las-Vegas_NV_89148_M14497-02317",
        "https://www.realtor.com/realestateandhomes-detail/2700-Las-Vegas-Blvd-S-Unit-3604_Las-Vegas_NV_89109_M12056-23357"
    ],
    "search": "Las Vegas",
    "mode": "BUY",
    "proxy": {
        "useApifyProxy": true
    },
    "maxItems": 5
}
```

## During the Run

During the run, the actor will output messages letting you know what is going on. Each message always contains a short label specifying which page from the provided list is currently specified.
When items are loaded from the page, you should see a message about this event with a loaded item count and total item count for each page.

If you provide incorrect input to the actor, it will immediately stop with failure state and output an explanation of what is wrong.

## Realtor Export

During the run, the actor stores results into a dataset. Each item is a separate item in the dataset.

You can manage the results in any languague (Python, PHP, Node JS/NPM). See the FAQ or <a href="https://www.apify.com/docs/api" target="blank">our API reference</a> to learn more about getting results from this Realtor actor.

## Scraped Realtor Properties

The structure of each item in Realtor products looks like this:

###Sold Properties

```json
{
    "url": "https://www.realtor.com/realestateandhomes-detail/2700-Las-Vegas-Blvd-S-Unit-3604_Las-Vegas_NV_89109_M12056-23357",
    "type": "Sold",
    "soldOn": "March  1, 2021",
    "price": {
        "low": 319000,
        "high": 319000
    },
    "beds": "2",
    "baths": "2",
    "sqft": "1,100",
    "address": {
        "street": "2700 Las Vegas Blvd S Unit 3604,",
        "locality": "Las Vegas",
        "region": "NV",
        "postalCode": "89109"
    },
    "photos": [
        "https://ap.rdcpix.com/f45992b5ca48afac9a9ff447d1ad0e06l-m3433523426xd-w1020_h770_q80.jpg",
        "https://ap.rdcpix.com/f45992b5ca48afac9a9ff447d1ad0e06l-m2960903669xd-w1020_h770_q80.jpg",
        "https://ap.rdcpix.com/f45992b5ca48afac9a9ff447d1ad0e06l-m1139842363xd-w1020_h770_q80.jpg",
        "https://ap.rdcpix.com/f45992b5ca48afac9a9ff447d1ad0e06l-m2689214255xd-w1020_h770_q80.jpg",
        "https://ap.rdcpix.com/f45992b5ca48afac9a9ff447d1ad0e06l-m3524626986xd-w1020_h770_q80.jpg",
        "https://ap.rdcpix.com/f45992b5ca48afac9a9ff447d1ad0e06l-m2848963819xd-w1020_h770_q80.jpg",
        "https://ap.rdcpix.com/f45992b5ca48afac9a9ff447d1ad0e06l-m2411300949xd-w1020_h770_q80.jpg",
        "https://ap.rdcpix.com/f45992b5ca48afac9a9ff447d1ad0e06l-m804131764xd-w1020_h770_q80.jpg",
        "https://ap.rdcpix.com/f45992b5ca48afac9a9ff447d1ad0e06l-m3758438252xd-w1020_h770_q80.jpg",
        "https://ap.rdcpix.com/f45992b5ca48afac9a9ff447d1ad0e06l-m2102570235xd-w1020_h770_q80.jpg",
        "https://ap.rdcpix.com/f45992b5ca48afac9a9ff447d1ad0e06l-m173675823xd-w1020_h770_q80.jpg",
        "https://ap.rdcpix.com/f45992b5ca48afac9a9ff447d1ad0e06l-m3887120529xd-w1020_h770_q80.jpg",
        "https://ap.rdcpix.com/f45992b5ca48afac9a9ff447d1ad0e06l-m838061303xd-w1020_h770_q80.jpg",
        "https://ap.rdcpix.com/f45992b5ca48afac9a9ff447d1ad0e06l-m956392587xd-w1020_h770_q80.jpg",
        "https://ap.rdcpix.com/f45992b5ca48afac9a9ff447d1ad0e06l-m3440719059xd-w1020_h770_q80.jpg",
        "https://ap.rdcpix.com/f45992b5ca48afac9a9ff447d1ad0e06l-m2068669946xd-w1020_h770_q80.jpg",
        "https://ap.rdcpix.com/f45992b5ca48afac9a9ff447d1ad0e06l-m2909057827xd-w1020_h770_q80.jpg",
        "https://ap.rdcpix.com/f45992b5ca48afac9a9ff447d1ad0e06l-m334569709xd-w1020_h770_q80.jpg",
        "https://ap.rdcpix.com/f45992b5ca48afac9a9ff447d1ad0e06l-m3081227089xd-w1020_h770_q80.jpg",
        "https://ap.rdcpix.com/f45992b5ca48afac9a9ff447d1ad0e06l-m636682407xd-w1020_h770_q80.jpg",
        "https://ap.rdcpix.com/f45992b5ca48afac9a9ff447d1ad0e06l-m1669221286xd-w1020_h770_q80.jpg",
        "https://ap.rdcpix.com/f45992b5ca48afac9a9ff447d1ad0e06l-m492254240xd-w1020_h770_q80.jpg",
        "https://ap.rdcpix.com/f45992b5ca48afac9a9ff447d1ad0e06l-m1800078129xd-w1020_h770_q80.jpg",
        "https://ap.rdcpix.com/f45992b5ca48afac9a9ff447d1ad0e06l-m3866255466xd-w1020_h770_q80.jpg",
        "https://ap.rdcpix.com/f45992b5ca48afac9a9ff447d1ad0e06l-m3211244585xd-w1020_h770_q80.jpg",
        "https://ap.rdcpix.com/f45992b5ca48afac9a9ff447d1ad0e06l-m3955207768xd-w1020_h770_q80.jpg",
        "https://ap.rdcpix.com/f45992b5ca48afac9a9ff447d1ad0e06l-m616016766xd-w1020_h770_q80.jpg",
        "https://ap.rdcpix.com/f45992b5ca48afac9a9ff447d1ad0e06l-m2511157008xd-w1020_h770_q80.jpg",
        "https://ap.rdcpix.com/f45992b5ca48afac9a9ff447d1ad0e06l-m285756502xd-w1020_h770_q80.jpg",
        "https://ap.rdcpix.com/f45992b5ca48afac9a9ff447d1ad0e06l-m1026782433xd-w1020_h770_q80.jpg",
        "https://ap.rdcpix.com/f45992b5ca48afac9a9ff447d1ad0e06l-m1825795577xd-w1020_h770_q80.jpg",
        "https://ap.rdcpix.com/f45992b5ca48afac9a9ff447d1ad0e06l-m1327214018xd-w1020_h770_q80.jpg",
        "https://ap.rdcpix.com/f45992b5ca48afac9a9ff447d1ad0e06l-m1550604937xd-w1020_h770_q80.jpg",
        "https://ap.rdcpix.com/f45992b5ca48afac9a9ff447d1ad0e06l-m4035350925xd-w1020_h770_q80.jpg",
        "https://ap.rdcpix.com/f45992b5ca48afac9a9ff447d1ad0e06l-m2939373531xd-w1020_h770_q80.jpg",
        "https://ap.rdcpix.com/f45992b5ca48afac9a9ff447d1ad0e06l-m1576324972xd-w1020_h770_q80.jpg",
        "https://ap.rdcpix.com/f45992b5ca48afac9a9ff447d1ad0e06l-m1689968182xd-w1020_h770_q80.jpg",
        "https://ap.rdcpix.com/f45992b5ca48afac9a9ff447d1ad0e06l-m3028017238xd-w1020_h770_q80.jpg",
        "https://ap.rdcpix.com/f45992b5ca48afac9a9ff447d1ad0e06l-m3807718841xd-w1020_h770_q80.jpg",
        "https://ap.rdcpix.com/f45992b5ca48afac9a9ff447d1ad0e06l-m2013158385xd-w1020_h770_q80.jpg",
        "https://ap.rdcpix.com/f45992b5ca48afac9a9ff447d1ad0e06l-m3753635681xd-w1020_h770_q80.jpg",
        "https://ap.rdcpix.com/f45992b5ca48afac9a9ff447d1ad0e06l-m750831483xd-w1020_h770_q80.jpg",
        "https://ap.rdcpix.com/f45992b5ca48afac9a9ff447d1ad0e06l-m3025805401xd-w1020_h770_q80.jpg",
        "https://ap.rdcpix.com/f45992b5ca48afac9a9ff447d1ad0e06l-m2622234092xd-w1020_h770_q80.jpg",
        "https://ap.rdcpix.com/f45992b5ca48afac9a9ff447d1ad0e06l-m3808681262xd-w1020_h770_q80.jpg",
        "https://ap.rdcpix.com/f45992b5ca48afac9a9ff447d1ad0e06l-m3970338978xd-w1020_h770_q80.jpg",
        "https://ap.rdcpix.com/f45992b5ca48afac9a9ff447d1ad0e06l-m2752466096xd-w1020_h770_q80.jpg",
        "https://ap.rdcpix.com/f45992b5ca48afac9a9ff447d1ad0e06l-m531841736xd-w1020_h770_q80.jpg"
    ],
    "breadcrumbs": ["Nevada", "Clark County", "Las Vegas", "Las-Vegas Blvd"],
    "nearbySchools": [
        {
            "rating": 5,
            "name": "John S Park Elementary School",
            "grades": "PK–5",
            "distance": "1.5 mi"
        },
        {
            "rating": 5,
            "name": "John C  Fremont Middle School",
            "grades": "6–8",
            "distance": "1.4 mi"
        },
        {
            "rating": 4,
            "name": "Ed W Clark High School",
            "grades": "9–12",
            "distance": "2.0 mi"
        },
        {
            "rating": 4,
            "name": "Rex Bell Elementary School",
            "grades": "PK–5",
            "distance": "1.1 mi"
        },
        {
            "rating": 3,
            "name": "Innovations International Charter School of NV",
            "grades": "6–12",
            "distance": "2.0 mi"
        },
        {
            "rating": 10,
            "name": "Las Vegas Academy Of Int'l Studies  Performing And School",
            "grades": "9–12",
            "distance": "2.2 mi"
        },
        {
            "rating": null,
            "name": "Trinity Christian Private Schools",
            "grades": "PK–6",
            "distance": "1.2 mi"
        },
        {
            "rating": null,
            "name": "Academy For Learning Private School",
            "grades": "K–12",
            "distance": "1.3 mi"
        }
    ],
    "neighborhood": {
        "Median Listing Price": "$324,900",
        "Price Per Sq Ft": "$187"
    },
    "overview": {
        "Status": "Sold",
        "Price/Sq Ft": "$290",
        "Type": "Condo/Townhome/Row Home/Co-Op",
        "Built": "2006"
    },
    "marketSummary": [
        {
            "label": "Less expensive than nearby properties",
            "value": "1.82%"
        },
        {
            "label": "Neighborhood Median Price",
            "value": "$324,900"
        },
        {
            "label": "Days since last sold",
            "value": "17"
        }
    ],
    "publicRecords": [
        "Beds: 2",
        "Rooms: 4",
        "House size: 1,100 sq ft",
        "Stories: 1",
        "Heating: Forced Air",
        "Cooling: Central",
        "Year built: 2006",
        "Year renovated: 2006",
        "Property type: Condo",
        "Style: Condo/Apartment",
        "Date updated: 03/12/2021"
    ]
}
```

###For Sale Properties

```json
{
    "url": "https://www.realtor.com/realestateandhomes-detail/9101-Alta-Dr-Unit-304_Las-Vegas_NV_89145_M24672-57224",
    "type": "For Sale",
    "price": {
        "low": 1500000,
        "high": 1500000
    },
    "beds": "3",
    "baths": "3.5",
    "sqft": "3,100",
    "sqftlot": "",
    "coordinates": {
        "latitude": "36.166961",
        "longitude": "-115.291125"
    },
    "address": {
        "address": "9101 Alta Dr Unit 304, Las Vegas, NV, 89145"
    },
    "photos": [
        "https://ap.rdcpix.com/b04156c06d4cfb4e4b2164b7688c8a9cl-m2895103670od-w1024_h768.jpg",
        "https://ap.rdcpix.com/b04156c06d4cfb4e4b2164b7688c8a9cl-m3563180654od-w1024_h768.jpg",
        "https://ap.rdcpix.com/b04156c06d4cfb4e4b2164b7688c8a9cl-m2895103670od-w1024_h768.jpg",
        "https://ap.rdcpix.com/b04156c06d4cfb4e4b2164b7688c8a9cl-m3563180654od-w1024_h768.jpg",
        "https://ap.rdcpix.com/b04156c06d4cfb4e4b2164b7688c8a9cl-m2895103670od-w1024_h768.jpg",
        "https://ap.rdcpix.com/b04156c06d4cfb4e4b2164b7688c8a9cl-m3563180654od-w1024_h768.jpg"
    ],
    "breadcrumbs": [
        "Nevada",
        "Clark County",
        "Las Vegas",
        "9101 Alta Dr Unit 304"
    ],
    "nearbySchools": [
        {
            "rating": 9,
            "name": "John W Bonner Elementary School",
            "grades": "PK - 5",
            "distance": "2.1"
        },
        {
            "rating": 7,
            "name": "Palo Verde High School",
            "grades": "9 - 12",
            "distance": "2.3"
        },
        {
            "rating": 8,
            "name": "Sig Rogich Middle School",
            "grades": "6 - 8",
            "distance": "2.6"
        }
    ],
    "overview": {
        "Property Type": "Condo",
        "Days on Realtor.com": "29 Days",
        "Year Built": "2006",
        "Price per sqft": "$484",
        "Status": "For Sale"
    },
    "description": "Incredible Lemar Efaw 3rd floor trophy home. This 3, 100 sqft home features a 3 bed 3.5 bath floor plan with den! This home has been treated to world class upgrades including petrified wood inlaid tile, custom lighting fixtures, custom horizontal fireplace, bespoke wall treatments & more. Custom tile work includes leather & glass beaded selections. The owners suite offers gorgeous mountain views & an extended walk in closet. A gourmet chef kitchen with crisp white cabinetry, contrasting island & SS appliance suite. Updated LED lighting adorn each room with custom ceiling soffits, custom built-ins & a full-size washer & dryer. This home is complete with a 2 car enclosed garage.One Queensridge Place offers resort style amenities with daily complimentary coffee bar, in/out pool & spa, billiards, conference & media room, wine cellar & Poker room. Fitness center featured Pilates/Yoga studio & Men & Womens Roman style spa with steam & sauna.",
    "features": [
        {
            "label": "Bedrooms",
            "values": ["Bedrooms: 3"]
        },
        {
            "label": "Other Rooms",
            "values": ["Total Rooms: 7"]
        },
        {
            "label": "Bathrooms",
            "values": [
                "Total Bathrooms: 4",
                "Full Bathrooms: 2",
                "1/2 Bathrooms: 1",
                "3/4 Bathrooms: 1"
            ]
        },
        {
            "label": "Appliances",
            "values": [
                "Dishwasher",
                "Dryer",
                "Garbage Disposer",
                "Microwave",
                "Refrigerator",
                "Refrigerator - Wine Storage",
                "Washer"
            ]
        },
        {
            "label": "Heating and Cooling",
            "values": ["Heating Features: Fireplace"]
        },
        {
            "label": "Interior Features",
            "values": ["Flooring: Tile - Stone, Tile or Stone"]
        },
        {
            "label": "Garage and Parking",
            "values": ["Parking Features: Valet"]
        },
        {
            "label": "Home Features",
            "values": ["View: City, Mountain"]
        },
        {
            "label": "Other Property Info",
            "values": [
                "Annual Tax Amount: 8314",
                "County: Clark County",
                "Directions: From Summerlin Parkway and Rampart Blvd. South on Rampart. Right (West) on Alta Drive. Left (South) at One Queensridge Place community entrance.",
                "Source Property Type: Common Interest",
                "Property Subtype: condo",
                "Source Neighborhood: One Queensridge Place Phase 1",
                "Parcel Number: 138-32-213-029",
                "Subdivision: One Queensridge Place Phase 1",
                "Property Subtype: Condominium",
                "Source System Name: C2C"
            ]
        },
        {
            "label": "Building and Construction",
            "values": ["Year Built: 2006", "Property Age: 15"]
        }
    ],
    "neighborhood": {
        "Median Listing Price": "$795,000",
        "Price Per Sq Ft": "$241"
    }
}
```

###Rental Properties

```json
{
    "url": "https://www.realtor.com/realestateandhomes-detail/6655-S-Fort-Apache-Rd_Las-Vegas_NV_89148_M14497-02317",
    "type": "Rental",
    "price": {
        "low": 1256,
        "high": 1509
    },
    "beds": "1 - 2",
    "baths": "1 - 2",
    "sqft": "749 - 1,212",
    "pets": "Pets",
    "coordinates": {
        "latitude": "36.067561",
        "longitude": "-115.298376"
    },
    "address": {
        "name": "MARTIN APARTMENT HOMES",
        "street": "6655 S Fort Apache Rd,6655 S Fort Apache Rd",
        "locality": "Las VegasLas Vegas",
        "region": "NVNV",
        "postalCode": "8914889148"
    },
    "photos": [
        "https://ar.rdcpix.com/ce5b316f0a2359dc90215bb9c77d21a9c-f2123701071xd-w1020_h770_q80.jpg",
        "https://ar.rdcpix.com/ce5b316f0a2359dc90215bb9c77d21a9c-f1534942297xd-w1020_h770_q80.jpg",
        "https://ar.rdcpix.com/ce5b316f0a2359dc90215bb9c77d21a9c-f878652904xd-w1020_h770_q80.jpg",
        "https://ar.rdcpix.com/ce5b316f0a2359dc90215bb9c77d21a9c-f731565892xd-w1020_h770_q80.jpg",
        "https://ar.rdcpix.com/ce5b316f0a2359dc90215bb9c77d21a9c-f1266638027xd-w1020_h770_q80.jpg",
        "https://ar.rdcpix.com/ce5b316f0a2359dc90215bb9c77d21a9c-f3306876858xd-w1020_h770_q80.jpg",
        "https://ar.rdcpix.com/ce5b316f0a2359dc90215bb9c77d21a9c-f3594548308xd-w1020_h770_q80.jpg",
        "https://ar.rdcpix.com/ce5b316f0a2359dc90215bb9c77d21a9c-f1628626175xd-w1020_h770_q80.jpg",
        "https://ar.rdcpix.com/ce5b316f0a2359dc90215bb9c77d21a9c-f3750668450xd-w1020_h770_q80.jpg",
        "https://ar.rdcpix.com/ce5b316f0a2359dc90215bb9c77d21a9c-f684007143xd-w1020_h770_q80.jpg",
        "https://ar.rdcpix.com/ce5b316f0a2359dc90215bb9c77d21a9c-f2833146668xd-w1020_h770_q80.jpg",
        "https://ar.rdcpix.com/ce5b316f0a2359dc90215bb9c77d21a9c-f638103031xd-w1020_h770_q80.jpg",
        "https://ar.rdcpix.com/ce5b316f0a2359dc90215bb9c77d21a9c-f3355794822xd-w1020_h770_q80.jpg",
        "https://ar.rdcpix.com/ce5b316f0a2359dc90215bb9c77d21a9c-f1380261674xd-w1020_h770_q80.jpg",
        "https://ar.rdcpix.com/ce5b316f0a2359dc90215bb9c77d21a9c-f2554417832xd-w1020_h770_q80.jpg",
        "https://ar.rdcpix.com/ce5b316f0a2359dc90215bb9c77d21a9c-f3728746811xd-w1020_h770_q80.jpg",
        "https://ar.rdcpix.com/ce5b316f0a2359dc90215bb9c77d21a9c-f872673047xd-w1020_h770_q80.jpg",
        "https://ar.rdcpix.com/ce5b316f0a2359dc90215bb9c77d21a9c-f3693420232xd-w1020_h770_q80.jpg",
        "https://ar.rdcpix.com/ce5b316f0a2359dc90215bb9c77d21a9c-f2117598234xd-w1020_h770_q80.jpg",
        "https://ar.rdcpix.com/ce5b316f0a2359dc90215bb9c77d21a9c-f2438733769xd-w1020_h770_q80.jpg",
        "https://ar.rdcpix.com/ce5b316f0a2359dc90215bb9c77d21a9c-f2289071579xd-w1020_h770_q80.jpg",
        "https://ar.rdcpix.com/ce5b316f0a2359dc90215bb9c77d21a9c-f46009409xd-w1020_h770_q80.jpg",
        "https://ar.rdcpix.com/ce5b316f0a2359dc90215bb9c77d21a9c-f1762979708xd-w1020_h770_q80.jpg",
        "https://ar.rdcpix.com/ce5b316f0a2359dc90215bb9c77d21a9c-f1213514775xd-w1020_h770_q80.jpg",
        "https://ar.rdcpix.com/ce5b316f0a2359dc90215bb9c77d21a9c-f2176171169xd-w1020_h770_q80.jpg",
        "https://ar.rdcpix.com/ce5b316f0a2359dc90215bb9c77d21a9c-f152252890xd-w1020_h770_q80.jpg",
        "https://ar.rdcpix.com/ce5b316f0a2359dc90215bb9c77d21a9c-f527547253xd-w1020_h770_q80.jpg",
        "https://ar.rdcpix.com/ce5b316f0a2359dc90215bb9c77d21a9c-f3655246583xd-w1020_h770_q80.jpg",
        "https://ar.rdcpix.com/ce5b316f0a2359dc90215bb9c77d21a9c-f682254238xd-w1020_h770_q80.jpg",
        "https://ar.rdcpix.com/ce5b316f0a2359dc90215bb9c77d21a9c-f3270340978xd-w1020_h770_q80.jpg",
        "https://ar.rdcpix.com/ce5b316f0a2359dc90215bb9c77d21a9c-f1552785935xd-w1020_h770_q80.jpg",
        "https://ar.rdcpix.com/ce5b316f0a2359dc90215bb9c77d21a9c-f711105821xd-w1020_h770_q80.jpg",
        "https://ar.rdcpix.com/ce5b316f0a2359dc90215bb9c77d21a9c-f3919044809xd-w1020_h770_q80.jpg",
        "https://ar.rdcpix.com/ce5b316f0a2359dc90215bb9c77d21a9c-f2003418685xd-w1020_h770_q80.jpg"
    ],
    "breadcrumbs": [
        "Nevada",
        "Clark County",
        "Las Vegas",
        "6655 S Fort Apache Rd"
    ],
    "features": [
        {
            "title": "Community Features",
            "values": [
                "* In Select Homes",
                "* Per plan, see leasing associate for details",
                "** Some restrictions apply.",
                "24 Hour Pool",
                "24-hour emergency maintenance services",
                "4 single-level floor plans",
                "Adult-height vanity with full-size mirror",
                "Air Conditioning",
                "Balcony",
                "Cabana",
                "Cable Ready",
                "Car Wash Area",
                "Carpet",
                "Cats Allowed",
                "Ceiling Fans",
                "Community BBQ",
                "Complimentary daily refreshments and coffee bar",
                "Controlled Access",
                "Courtesy Patrol",
                "Designer-selected interior color schemes",
                "Detached & Direct Access Garages Offered",
                "Digital programmable thermostat",
                "Dining Room",
                "Dishwasher",
                "Disposal",
                "Dogs Allowed",
                "Double Pane Windows",
                "Easy care granite-look laminate countertops",
                "Energy efficient low E dual glazed windows",
                "Faux wood blinds on most windows",
                "Fitness Center",
                "Fitness Center",
                "Frameless medicine cabinet",
                "Freezer",
                "Gated",
                "Grill",
                "Hardwood Floors",
                "Heating",
                "High Speed Internet Access",
                "Ice Maker",
                "Impressive 9' volume ceilings*",
                "Kitchen",
                "Large garden style soaking tub with shower",
                "Linen Closet",
                "Linen, coat and storage closets*",
                "Lounge",
                "Lush entry common area landscaping",
                "Media Center/Movie Theatre",
                "Media Room",
                "Microwave",
                "Mountain and city views*",
                "Multi Use Room",
                "One and two bedroom plans",
                "Online Payments Available",
                "Oven",
                "Oversized closets",
                "Package Service",
                "Pantry",
                "Patio",
                "Pool",
                "Premium GE® appliances package",
                "Print & Connect",
                "Private direct access garages*",
                "Private patios and balconies*",
                "Property Manager on Site",
                "Range",
                "Recycling",
                "Renters Insurance Program",
                "Resident activities",
                "Security System",
                "Security alarm system",
                "Smoke Detectors",
                "Spa",
                "Spa Shower",
                "Sprinkler System",
                "Stylish cabinetry with polished chrome hardware",
                "Trash Pickup - Door to Door",
                "Tub/Shower",
                "Views",
                "Vinyl Flooring",
                "Washer/Dryer",
                "Wi-Fi",
                "Wi-Fi at Pool and Clubhouse"
            ]
        },
        {
            "title": "Unit Features",
            "values": [
                "Air Conditioning",
                "Cable or Satellite TV",
                "Carport",
                "Ceiling Fan",
                "Courtyard",
                "Dishwasher",
                "Disposal",
                "Garage",
                "Microwave",
                "Patio/Balcony",
                "Refrigerator",
                "View"
            ]
        },
        {
            "title": "Local Home Services",
            "values": []
        }
    ],
    "nearbySchools": [
        {
            "rating": 5,
            "name": "Wayne N Tanaka Elementary School",
            "grades": "PK–5",
            "distance": "0.5 mi"
        },
        {
            "rating": 6,
            "name": "Wilbur & Theresa Faiss Middle School",
            "grades": "6–8",
            "distance": "0.4 mi"
        },
        {
            "rating": 4,
            "name": "Sierra Vista High School",
            "grades": "9–12",
            "distance": "2.0 mi"
        },
        {
            "rating": 8,
            "name": "Kathy L. Batterman Elementary School",
            "grades": "PK–5",
            "distance": "1.3 mi"
        },
        {
            "rating": null,
            "name": "American Preparatory Academy School",
            "grades": "K–12",
            "distance": "1.5 mi"
        },
        {
            "rating": 4,
            "name": "Durango High School",
            "grades": "9–12",
            "distance": "3.2 mi"
        },
        {
            "rating": null,
            "name": "Bishop Gorman Private School",
            "grades": "9–12",
            "distance": "1.5 mi"
        },
        {
            "rating": null,
            "name": "Merryhill Elementary Private School",
            "grades": "K–5",
            "distance": "2.3 mi"
        }
    ],
    "neighborhood": {
        "Median Rental Price": "$1,600",
        "Median Listing Price": "$324,900"
    },
    "overview": {
        "leaseTerms": "None",
        "listingManagedBy": "FPI Management",
        "Type": "Apartment",
        "Built": "2016"
    },
    "description": "Situated in a sophisticated and beautiful premier neighborhood, Martin offers a gated entry, a selection of apartment homes with views of the mountains and the exciting Las Vegas Strip. It is ideally located in the heart of it all and just minutes from a variety of restaurants, eclectic boutiques, shopping centers, conveniences, and even the Wet-n-Wild theme park. Martin's collection of stylish 1 and 2 bedroom homes features stylish interiors with the latest finishes including sleek cabinetry, black energy-efficient appliances, granite-look countertops, and oversized windows. You'll enjoy a resort-style pool with cabana, fitness center and the W Lounge, where you can relax and socialize with friends and even get free Wi-Fi! Martin Apartment Home is professionally managed by FPI.",
    "floorPlans": [
        {
            "title": "1 Bedroom (1 plan )",
            "plans": [
                {
                    "name": "Chaparral",
                    "bath": "1 ba",
                    "sqft": "749 sq ft",
                    "price": "$1,256",
                    "availability": "Available in April 2021"
                }
            ]
        },
        {
            "title": "2 Bedroom (3 plans )",
            "plans": [
                {
                    "name": "Avalon",
                    "bath": "2 ba",
                    "sqft": "1,212 sq ft",
                    "price": "$1,424",
                    "availability": "Available"
                },
                {
                    "name": "Carson",
                    "bath": "2 ba",
                    "sqft": "1,203 sq ft",
                    "price": "$1,505",
                    "availability": "Available in March 2021"
                },
                {
                    "name": "Aurora",
                    "bath": "2 ba",
                    "sqft": "1,016 sq ft",
                    "price": "$1,509",
                    "availability": "Check Availability"
                }
            ]
        }
    ]
}
```
