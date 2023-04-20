# Actor - Lobsters Scraper

## Lobsters scraper

Since Lobste.rs doesn't provide a good and free API, this actor should help you to retrieve data from it.

The Lobsters data scraper supports the following features:

-   Search any keyword - You can search any keyword you would like to have and get the results

-   Scrape domains - Get all the posts from each of the domains that is represented in lobste.rs.

-   Get posts by tags - Scraping the results by a certain tag is definitely doable!

-   Retrieve user detail - If you are looking for a specific user details, you are in the right place.

-   Fetch comments of any post - All the comments that has been shared under a post are also included inside the search results.

-   Get active and recent posts - Don't get outdated! Active and recent posts can be harvested right away from the Lobsters.

## Bugs, fixes, updates and changelog

This scraper is under active development. If you have any feature requests you can create an issue from [here](https://github.com/epctex/lobsters-scraper/issues).

## Input Parameters

The input of this scraper should be JSON containing the list of pages on Lobsters that should be visited. Required fields are:

| Field                | Type    | Description                                                                                                                                                                                                    |
| -------------------- | ------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| search               | String  | (optional) Keyword that you want to search on Lobsters.                                                                                                                                                       |
| startUrls            | Array   | (optional) List of Lobsters URLs. You should only provide domains, tags, user detail, post detail, active posts, recent posts, or search URLs                                                                                                                 |
| endPage              | Integer | (optional) Final number of page that you want to scrape. Default is `Infinite`. This is applies to all `search` request and `startUrls` individually.                                                          |
| maxItems             | Integer | (optional) You can limit scraped items. This should be useful when you search through the big lists or search results.                                                                                                |
| proxy                | Object  | Proxy configuration                                                                                                                                                                                            |
| extendOutputFunction | String  | (optional) Function that takes a JQuery handle ($) as argument and returns object with data                                                                                                                    |
| customMapFunction | String  | (optional) Function that takes each objects handle as argument and returns object with executing the function                                                                                                                     |

This solution requires the use of **Proxy servers**, either your own proxy servers or you can use [Apify Proxy](https://www.apify.com/docs/proxy).

##### Tip

When you want to have a scrape over a specific list URL, just copy and paste the link as one of the **startUrl**.

If you would like to scrape only the first page of a list then put the link for the page and have the `endPage` as 1.

With the last approach that explained above you can also fetch any interval of pages. If you provide the 5th page of a list and define the `endPage` parameter as 6 then you'll have the 5th and 6th pages only.

### Compute Unit Consumption

The actor optimized to run blazing fast and scrape as many items as possible. Therefore, it forefronts all the detail requests. If actor doesn't block very often it'll scrape 100 listings in 30 seconds with ~0.01-0.02 compute units.

### Lobsters Scraper Input example

```json
{
 "startUrls": [
  "https://lobste.rs/domains/google.com",
  "https://lobste.rs/t/devops",
  "https://lobste.rs/u/lambda",
  "https://lobste.rs/active",
  "https://lobste.rs/recent",
  "https://lobste.rs/search?q=google&what=stories&order=newest"
 ],
 "maxItems":10,
 "endPage":2,
  "proxy":{
    "useApifyProxy":true
  }
}

```

## During the Run

During the run, the actor will output messages letting you know what is going on. Each message always contains a short label specifying which page from the provided list is currently specified.
When items are loaded from the page, you should see a message about this event with a loaded item count and total item count for each page.

If you provide incorrect input to the actor, it will immediately stop with failure state and output an explanation of what is wrong.

## Lobsters Export

During the run, the actor stores results into a dataset. Each item is a separate item in the dataset.

You can manage the results in any languague (Python, PHP, Node JS/NPM). See the FAQ or <a href="https://www.apify.com/docs/api" target="blank">our API reference</a> to learn more about getting results from this Lobsters actor.

## Scraped Lobsters Properties

The structure of each item in Lobsters looks like this:

### User Detail

```json
{
	"type": "user",
	"name": "lambda",
	"url": "https://lobste.rs/u/lambda",
	"avatar": "https://lobste.rs/avatars/lambda-100.png",
	"status": "Active user",
	"homepage": "https://maxcountryman.com",
	"github": "https://github.com/maxcountryman",
	"twitter": "https://twitter.com/MaxCountryman",
	"about": "Indie hacker and people-first leader. Building https://remotejobs.com in public on Twitter.",
	"karma": "345, averaging 9.08 per story/comment",
	"numberOfComments": "10",
	"numberOfStories": "26, most commonly tagged compsci"
}
```

### Post Detail

```json
{
	"type": "post",
	"id": "kour63",
	"url": "https://lobste.rs/s/kour63/help_test_cargo_s_new_index_protocol",
	"title": "Help test Cargo's new index protocol",
	"link": "https://blog.rust-lang.org/inside-rust/2023/01/30/cargo-sparse-protocol.html",
	"numberOfUpvotes": 13,
	"userName": "icefox",
	"userLink": "https://lobste.rs/u/icefox",
	"domain": "blog.rust-lang.org",
	"date": "2023-03-09 12:24:32 -0600",
	"tags": [
		"devops",
		"rust"
	],
	"comments": [
		{
			"id": "dudcdn",
			"body": "Rust 1.68.0 has been released so this is now usable in stable Rust too. Still opt-in though. https://blog.rust-lang.org/2023/03/09/Rust-1.68.0.html",
			"numberOfUpvotes": 3,
			"date": "2023-03-09 16:48:32 -0600",
			"userLink": "https://lobste.rs/u/wezm",
			"userName": "wezmlink"
		}
	]
}
```
