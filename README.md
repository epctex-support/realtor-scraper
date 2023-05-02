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

-   Scrape listings of agents - Directly fetch any listing of agent profiles with ease!

#### Realtor specific

Don't worry when you get little bit different properties than you saw in browser page. Realtor is ordering properties differently for each user.

## Bugs, fixes, updates and changelog

This scraper is under active development. If you have any feature requests you can create an issue from [here](https://github.com/epctex/realtor-scraper/issues).

## Setup & Usage

You can see how this actor works in this video:


## Input Parameters

The input of this scraper should be JSON containing the list of pages on Realtor that should be visited. Possible fields are:

- `search`: (Optional) (String) Keyword that can be searched in Realtor search engine. When it is present, `mode` must be used as well.

- `startUrls`: (Optional) (Array) List of Realtor URLs. You should only provide property detail or search URLs.

- `mode`: (Optional) (String) Mode of the actor. It gets the keyword from `search` parameter and initiate the search according to the mode. Can be `BUY`, `RENT` or `SOLD`. When present, `search` must be provided as well.

- `endPage`: (Optional) (Number) Final number of page that you want to scrape. Default is `Infinite`. This is applies to all `search` request and `startUrls` individually.

- `maxItems`: (Optional) (Number) You can limit scraped items. This should be useful when you search through the big lists or search results.

- `proxy`: (Required) (Proxy Object) Proxy configuration.

- `extendOutputFunction`: (Optional) (String) Function that takes a JQuery handle ($) as argument and returns object with data.

This solution requires the use of **Proxy servers**, either your own proxy servers or you can use [Apify Proxy](https://www.apify.com/docs/proxy).

### Tip

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
        "https://www.realtor.com/realestateandhomes-detail/2700-Las-Vegas-Blvd-S-Unit-3604_Las-Vegas_NV_89109_M12056-23357",
        "https://www.realtor.com/realestateagents/5a28883df695ab0010dfe28b"
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

### Properties

```json
{
  "url": "https://www.realtor.com/realestateandhomes-detail/4368-Seville-St_Las-Vegas_NV_89121_M14226-64517",
  "status": "sold",
  "id": "1422664517",
  "soldOn": "2022-06-08",
  "lastSoldPrice": 485000,
  "listPrice": null,
  "baths": 3,
  "baths_3qtr": null,
  "baths_full": 2,
  "baths_full_calc": 2,
  "baths_half": 1,
  "baths_max": null,
  "baths_min": null,
  "baths_partial_calc": 1,
  "baths_total": 3,
  "beds": 4,
  "beds_max": null,
  "beds_min": null,
  "construction": null,
  "cooling": "Central",
  "exterior": "Frame/Stucco",
  "fireplace": "Yes",
  "garage": null,
  "garage_max": null,
  "garage_min": null,
  "garage_type": "Built In",
  "heating": "Forced Air",
  "logo": null,
  "lot_sqft": 9148,
  "name": null,
  "pool": null,
  "roofing": "Composition Shingle",
  "rooms": 9,
  "sqft": 2752,
  "sqft_max": null,
  "sqft_min": null,
  "stories": 2,
  "styles": null,
  "sub_type": null,
  "text": null,
  "type": "single_family",
  "units": null,
  "year_built": 1975,
  "year_renovated": 1975,
  "zoning": "R-1",
  "coordinates": {
    "latitude": 36.110005,
    "longitude": -115.077626
  },
  "address": {
    "street": "4368 Seville St",
    "locality": "Las Vegas",
    "region": "NV",
    "postalCode": "89121"
  },
  "photos": null,
  "nearbySchools": {
    "schools": [
      {
        "coordinate": {
          "lat": 36.11256,
          "lon": -115.072924
        },
        "distance_in_miles": 0.3,
        "district": {
          "id": "06188571441",
          "name": "Clark County School District"
        },
        "education_levels": [
          "elementary"
        ],
        "funding_type": "public",
        "grades": [
          "PK",
          "K",
          "1",
          "2",
          "3",
          "4",
          "5"
        ],
        "greatschools_id": "3200120",
        "id": "0745716001",
        "name": "William E  Ferron Elementary School",
        "nces_code": "320006000118",
        "parent_rating": 4,
        "rating": 5,
        "review_count": 7,
        "slug_id": "William-E-Ferron-Elementary-School-0745716001",
        "student_count": 647
      },
      {
        "coordinate": {
          "lat": 36.106733,
          "lon": -115.090665
        },
        "distance_in_miles": 0.8,
        "district": {
          "id": "06188571441",
          "name": "Clark County School District"
        },
        "education_levels": [
          "middle"
        ],
        "funding_type": "public",
        "grades": [
          "6",
          "7",
          "8"
        ],
        "greatschools_id": "3200020",
        "id": "0745714551",
        "name": "C W Woodbury Middle School",
        "nces_code": "320006000017",
        "parent_rating": 4,
        "rating": 2,
        "review_count": 9,
        "slug_id": "C-W-Woodbury-Middle-School-0745714551",
        "student_count": 904
      },
      {
        "coordinate": {
          "lat": 36.119938,
          "lon": -115.087966
        },
        "distance_in_miles": 0.9,
        "district": {
          "id": "06188571441",
          "name": "Clark County School District"
        },
        "education_levels": [
          "high"
        ],
        "funding_type": "public",
        "grades": [
          "9",
          "10",
          "11",
          "12"
        ],
        "greatschools_id": "3200021",
        "id": "0745714561",
        "name": "Chaparral High School",
        "nces_code": "320006000018",
        "parent_rating": 4,
        "rating": 3,
        "review_count": 7,
        "slug_id": "Chaparral-High-School-0745714561",
        "student_count": 2384
      },
      {
        "coordinate": {
          "lat": 36.117541,
          "lon": -115.092576
        },
        "distance_in_miles": 1,
        "district": {
          "id": "06188571421",
          "name": null
        },
        "education_levels": [
          "elementary",
          "middle"
        ],
        "funding_type": "private",
        "grades": [
          "K",
          "1",
          "2",
          "3",
          "4",
          "5",
          "6",
          "7",
          "8"
        ],
        "greatschools_id": "3200710",
        "id": "0745724421",
        "name": "Mt Olive Luteran School",
        "nces_code": "A0106133",
        "parent_rating": 5,
        "rating": null,
        "review_count": 4,
        "slug_id": "Mt-Olive-Luteran-School-0745724421",
        "student_count": 59
      }
    ]
  },
  "neighborhood": null,
  "local": {
    "flood": {
      "firststreet_url": "https://riskfactor.com/property/4368-seville-st-las-vegas-nevada-89121/321219289_fsid/flood?utm_source=realtor",
      "fsid": "321219289",
      "flood_factor_score": 1,
      "flood_factor_severity": "minimal",
      "environmental_risk": 1,
      "trend_direction": 0,
      "fema_zone": [
        "X"
      ],
      "insurance_requirement": "recommended",
      "flood_trend": "This property’s flood risk is not changing.",
      "flood_trend_paragraph": "This property’s risk of flood is <b>not changing</b>.",
      "flood_insurance_text": "As this property is located in FEMA Zone X, flood insurance is not federally required to obtain a mortgage. You may want to purchase flood insurance to protect your home. Explore quotes from <b>5 providers</b> that offer flood insurance from <b>$435</b> to <b>$905</b> per year.",
      "insurance_rates": [
        {
          "provider_url": "https://1str.ee/t/hippo/flood/321219289?source=realtor",
          "provider_name": "Hippo Insurance Agency, LLC",
          "provider_logo": "https://assets.floodfactor.com/insurance/hippo.png",
          "expires": null,
          "price": null,
          "home_coverage": 250000,
          "contents_coverage": 100000,
          "disclaimer": null
        }
      ]
    },
    "noise": {
      "score": 73,
      "noise_categories": [
        {
          "text": "Low",
          "type": "airport"
        },
        {
          "text": "High",
          "type": "traffic"
        },
        {
          "text": "Low",
          "type": "local"
        },
        {
          "text": "Medium",
          "type": "score"
        }
      ]
    },
    "wildfire": {
      "fsid": "321219289",
      "fire_factor_score": 1,
      "fire_factor_severity": "Minimal",
      "fire_cumulative_30": null,
      "fire_trend": "This property’s wildfire risk is not changing.",
      "fire_trend_paragraph": "This property's risk of wildfire is <b>not changing</b>.",
      "usfs_relative_risk": "This property is located in a county with an average wildfire risk greater than 85% counties in the US.",
      "firststreet_url": "https://riskfactor.com/property/4368-seville-st-las-vegas-nevada-89121/321219289_fsid/fire?utm_source=realtor",
      "fire_insurance_text": "Invest in insurance that covers hazards including wildfire to reduce your financial risk and recover more quickly after a fire. To protect your home, explore quotes from <b>7 providers</b> that offer insurance with wildfire coverage.",
      "insurance_rates": [
        {
          "provider_logo": "https://assets.floodfactor.com/insurance/hippo.png",
          "provider_url": "https://1str.ee/t/hippo/fire/321219289?source=realtor"
        }
      ]
    }
  },
  "history": [
    {
      "date": "2022-06-08",
      "event_name": "Sold",
      "price": 485000,
      "price_sqft": 176.23546511627907,
      "source_listing_id": null,
      "source_name": "Public Record",
      "listing": null
    },
    {
      "date": "2022-05-13",
      "event_name": "Listing removed",
      "price": 0,
      "price_sqft": null,
      "source_listing_id": "2393319",
      "source_name": "LasVegas",
      "listing": {
        "list_price": 475000,
        "last_status_change_date": "2022-05-13T03:08:06Z",
        "last_update_date": "2022-05-05T08:24:18Z",
        "status": "off_market",
        "list_date": "2022-05-05T08:04:46Z",
        "listing_id": "2942756233",
        "suppression_flags": {
          "has_suppress_sold_info": true
        },
        "photos": [
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m3082072648s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m1827141646s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m4254921847s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m1151405011s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m3806640650s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m3942876455s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m1661349441s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m4047814041s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m2160077492s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m1263782816s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m2746061833s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m4107406175s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m2910718438s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m3028123988s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m3813972027s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m1421957916s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m3431148020s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m3856479392s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m1411435325s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m491581803s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m2268681331s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m2922686144s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m2301519764s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m793117848s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m40245287s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m1936417894s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m3072168545s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m4212323395s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m202704110s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m563546097s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m1683360307s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m2833466280s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m341779919s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m2434645635s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m320319668s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m3619621644s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m690698608s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m593262984s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m2669032613s.jpg"
          }
        ],
        "description": {
          "text": "Spacious 2 Story, 4 Bed, 3 Bath, 2 car. Separate Dining, Family, and Living Room. RV Parking, 4 Car Spot Drive Way, Oversized 4th Bedroom Gym/Loft. Hard Wood Floor Upstairs, Tile Downstairs, Downstairs Laundry. Master Balcony, Above Ground Jacuzzi, Custom Shed, 9k Sqft lot Real Green Grass, Immaculate Landscaping. All Appliances to included."
        },
        "advertisers": [
          {
            "fulfillment_id": "2931320",
            "nrds_id": "629045097",
            "name": "Daron Rice",
            "email": "agentdrice@gmail.com",
            "href": "www.LvHouseListings.com",
            "slogan": "with the Jacobs Group",
            "office": {
              "fulfillment_id": "1211952",
              "name": "Simply Vegas",
              "email": "simplyvegasrealestate@gmail.com",
              "href": "",
              "slogan": "",
              "out_of_community": null,
              "application_url": null,
              "mls_set": "O-LVNV-SVRE"
            },
            "broker": {
              "fulfillment_id": "2931292",
              "name": "Simply Vegas",
              "accent_color": "#fc7b03",
              "logo": "https://ap.rdcpix.com/1974843881/951d73b0132029aff5898118d6e9729ak-c0s.jpg"
            },
            "type": "seller",
            "mls_set": "A-LVNV-226276"
          }
        ],
        "buyers": null,
        "source": {
          "id": "LVNV",
          "agents": [
            {
              "agent_id": "226276",
              "agent_name": "Daron Rice",
              "office_id": "SVRE",
              "office_name": null,
              "office_phone": null,
              "type": "seller"
            }
          ]
        }
      }
    },
    {
      "date": "2022-05-05",
      "event_name": "Listed",
      "price": 475000,
      "price_sqft": 172.60174418604652,
      "source_listing_id": "2393319",
      "source_name": "LasVegas",
      "listing": {
        "list_price": 475000,
        "last_status_change_date": "2022-05-13T03:08:06Z",
        "last_update_date": "2022-05-05T08:24:18Z",
        "status": "off_market",
        "list_date": "2022-05-05T08:04:46Z",
        "listing_id": "2942756233",
        "suppression_flags": {
          "has_suppress_sold_info": true
        },
        "photos": [
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m3082072648s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m1827141646s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m4254921847s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m1151405011s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m3806640650s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m3942876455s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m1661349441s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m4047814041s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m2160077492s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m1263782816s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m2746061833s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m4107406175s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m2910718438s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m3028123988s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m3813972027s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m1421957916s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m3431148020s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m3856479392s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m1411435325s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m491581803s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m2268681331s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m2922686144s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m2301519764s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m793117848s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m40245287s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m1936417894s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m3072168545s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m4212323395s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m202704110s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m563546097s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m1683360307s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m2833466280s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m341779919s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m2434645635s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m320319668s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m3619621644s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m690698608s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m593262984s.jpg"
          },
          {
            "href": "http://ap.rdcpix.com/804a9d1ab2622363f784ffddb59bdb93l-m2669032613s.jpg"
          }
        ],
        "description": {
          "text": "Spacious 2 Story, 4 Bed, 3 Bath, 2 car. Separate Dining, Family, and Living Room. RV Parking, 4 Car Spot Drive Way, Oversized 4th Bedroom Gym/Loft. Hard Wood Floor Upstairs, Tile Downstairs, Downstairs Laundry. Master Balcony, Above Ground Jacuzzi, Custom Shed, 9k Sqft lot Real Green Grass, Immaculate Landscaping. All Appliances to included."
        },
        "advertisers": [
          {
            "fulfillment_id": "2931320",
            "nrds_id": "629045097",
            "name": "Daron Rice",
            "email": "agentdrice@gmail.com",
            "href": "www.LvHouseListings.com",
            "slogan": "with the Jacobs Group",
            "office": {
              "fulfillment_id": "1211952",
              "name": "Simply Vegas",
              "email": "simplyvegasrealestate@gmail.com",
              "href": "",
              "slogan": "",
              "out_of_community": null,
              "application_url": null,
              "mls_set": "O-LVNV-SVRE"
            },
            "broker": {
              "fulfillment_id": "2931292",
              "name": "Simply Vegas",
              "accent_color": "#fc7b03",
              "logo": "https://ap.rdcpix.com/1974843881/951d73b0132029aff5898118d6e9729ak-c0s.jpg"
            },
            "type": "seller",
            "mls_set": "A-LVNV-226276"
          }
        ],
        "buyers": null,
        "source": {
          "id": "LVNV",
          "agents": [
            {
              "agent_id": "226276",
              "agent_name": "Daron Rice",
              "office_id": "SVRE",
              "office_name": null,
              "office_phone": null,
              "type": "seller"
            }
          ]
        }
      }
    }
  ],
  "taxHistory": [
    {
      "assessment": {
        "building": 32839,
        "land": 25900,
        "total": 58739
      },
      "market": {
        "building": 93826,
        "land": 74000,
        "total": 167826
      },
      "tax": 1176,
      "year": 2021
    },
    {
      "assessment": {
        "building": 33385,
        "land": 25200,
        "total": 58585
      },
      "market": {
        "building": 95386,
        "land": 72000,
        "total": 167386
      },
      "tax": 1089,
      "year": 2020
    },
    {
      "assessment": {
        "building": 33808,
        "land": 23100,
        "total": 56908
      },
      "market": {
        "building": 96594,
        "land": 66000,
        "total": 162594
      },
      "tax": 1057,
      "year": 2019
    },
    {
      "assessment": {
        "building": 32970,
        "land": 21700,
        "total": 54670
      },
      "market": {
        "building": 94200,
        "land": 62000,
        "total": 156200
      },
      "tax": 1026,
      "year": 2018
    },
    {
      "assessment": {
        "building": 34118,
        "land": 18200,
        "total": 52318
      },
      "market": {
        "building": 97480,
        "land": 52000,
        "total": 149480
      },
      "tax": 1534,
      "year": 2017
    },
    {
      "assessment": {
        "building": 35281,
        "land": 17500,
        "total": 52781
      },
      "market": {
        "building": 100803,
        "land": 50000,
        "total": 150803
      },
      "tax": 973,
      "year": 2016
    },
    {
      "assessment": {
        "building": 35502,
        "land": 12250,
        "total": 47752
      },
      "market": {
        "building": 101434,
        "land": 35000,
        "total": 136434
      },
      "tax": 970,
      "year": 2015
    },
    {
      "assessment": {
        "building": 34968,
        "land": 10500,
        "total": 45468
      },
      "market": {
        "building": 99909,
        "land": 30000,
        "total": 129909
      },
      "tax": 942,
      "year": 2014
    },
    {
      "assessment": {
        "building": 34850,
        "land": 6300,
        "total": 41150
      },
      "market": {
        "building": 99571,
        "land": 18000,
        "total": 117571
      },
      "tax": 992,
      "year": 2013
    },
    {
      "assessment": {
        "building": 23954,
        "land": 6300,
        "total": 30254
      },
      "market": {
        "building": 68440,
        "land": 18000,
        "total": 86440
      },
      "tax": 887,
      "year": 2012
    },
    {
      "assessment": {
        "building": 35179,
        "land": 7000,
        "total": 42179
      },
      "market": {
        "building": 100511,
        "land": 20000,
        "total": 120511
      },
      "tax": 1237,
      "year": 2011
    },
    {
      "assessment": {
        "building": 37267,
        "land": 7000,
        "total": 44267
      },
      "market": {
        "building": 106477,
        "land": 20000,
        "total": 126477
      },
      "tax": 1301,
      "year": 2010
    },
    {
      "assessment": {
        "building": 37189,
        "land": 36400,
        "total": 73589
      },
      "market": {
        "building": 106254,
        "land": 104000,
        "total": 210254
      },
      "tax": 1478,
      "year": 2008
    },
    {
      "assessment": {
        "building": 35597,
        "land": 41300,
        "total": 76897
      },
      "market": {
        "building": 101706,
        "land": 118000,
        "total": 219706
      },
      "tax": 1435,
      "year": 2007
    }
  ],
  "advertisers": null,
  "details": null
}
```
