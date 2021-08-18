# covbins
API to provide domestic bin collection dates for Coventry. Coventry City Council does not provide this data in a useful format for other applications, so here it is in REST. For example, I am building this to use it on a wall board by my front door to tell me when bin day is and which bins to ensure are available.

The following is currently what *will* happen, rather than what it actually does.

- A rate limited scrape of the [CCC Bin Collection Calendar](https://www.coventry.gov.uk/directory/82/bin_collection_calendar) is run at 0200 every day for all streets in Coventry.
- Data is transformed into JSON
- You can then `GET` the data you need.
- Bins are `brown`, `blue`, `green` or `unknown` for addresses that do not specify lid colours.

GET http://api.jamesgeddes.pro/covbins/{street}/{doornumber}

Returns all known bin collection dates for your address and which bins are to be collected.

GET http://api.jamesgeddes.pro/covbins/{street}/{doornumber}/{date}

Returns the bins that are to be/were collected at this address on the specified yyyymmdd format {date}.

You could, for example, run `GET http://api.jamesgeddes.pro/covbins/{your street}/{your doornumber}/{date tomorrow}` each afternoon to tell you which bins to prepare for the next morning.



**Constraints**

- Data is out of date by at most 24 hours.
- Calls are currently answered by a Raspberry Pi, so requests are rate limited to 1 per minute so that you don't caramelise it.
- If you would like to make many requests per day, GitHub sponsorship would be very much appreciated. You could also ask your local [Councillor](https://www.coventry.gov.uk/councillors/search) to get this service adopted by CCC