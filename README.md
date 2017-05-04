# Technical test for Fotocasa backend developer

(For how to deliver this test, check [DELIVERABLE.md](DELIVERABLE.md))

This public service handles a list of tweets, each of 140 characters or less. The service
can be described with the following user stories and acceptance criteria:

* As a User, I want to publish a Tweet.
    * A Tweet can't be empty.
    * A Tweet can't contain more than 140 characters.
    * A Tweet's Publisher name can't be empty.

* As a User, I want to view the list of published Tweets.
    * The list must be sorted by publication date in descending order.
     
To pass this test, we expect software that also fulfills the following list of strategic user stories

* As a User, I want to add links to the tweet text without affecting the 140 character limit.
    * A link is any set of non-whitespace consecutive characters starting with http:// or https:// and finishing with a space.
        * For example, the tweet `Hey http://foogle.co` is 4 characters long, instead of 20.
* As a User, I want to discard tweets.
    * Tweets shall be discarded globally, we don't need user-based discarding.
    * Discarded tweets will not be shown in the published tweet list.
* As a User, I want to view a list of discarded tweets.
    * The list must be sorted by the date it was discarded on in descending order.

## Technical Requirements

* The application must fulfill all of the acceptance criteria.
* Feel free to refactor old code when adding new user stories.
* Application test coverage must not decrease.
* Do not use any framework or library not already in the codebase.
* API contracts can't be changed or modified any way.

### APIs

For the two new endpoints, you must accept this API:

* As a User, I want to discard tweets:
    * POST /discarded
    * Content-Type: application/json
    * `{ "tweet": "%TWEET_ID%" }` 
    
* As a User, I want to view a list of discarded tweets:
    * GET /discarded
    * The response body format should be identical to the published tweets GET /tweet endpoint.
        * New fields are not allowed.

All other endpoint contracts must not be changed.

## Usage

From the application folder, run
```sh
./gradlew bootRun
```

To get all published tweets
```sh
curl http://localhost:8080/tweet
```

To publish a new tweet
```sh
curl -XPOST -d '{ "publisher": "Prospect", "tweet": "Breaking the law" }' -H 'Content-Type: application/json' http://localhost:8080/tweet
```

## Test

From the application folder, run
```sh
./gradlew test
```
