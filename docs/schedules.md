## Schedules

The `/schedules` endpoint provides access to schedule information.  Results are ordered by `start_at` and filtered to `scheduled_after` the current time by default.

* [Request and Response](#request-and-response)
* [Pagination](#pagination)
* [Filters](#filters)
* [Sorting](#sorting)
* [Facets](#facets)

## Request and Response

### Request

`GET /schedules`

### Response Fields

| Field | Type | Notes |
| --- | --- | --- |
| assoc_id | integer | ID of the Association |
| assoc_name | text | Name of the association (ex. "YMCA of Greater Wichita") |
| branch_id | integer | Numerical ID of the branch |
| branch_name | text | Name of the branch (ex. "Ken Shannon Northwest YMCA") |
| branch_time_zone | text |  |
| category_id | integer | Numerical ID of the program category |
| category_label | text | Name of the program category (ex. "Cardio") |
| description | text | Program description (ex. "Slim, trim and strengthen your body using a variety of equipment for both upper and lower body. No cardio involved.") |
| duration | integer | Duration in seconds |
| end_at  | datetime | Occurrence end time (when instruction ends). In ISO 8601 format. |
| event_id | integer | ID of the event |
| get_ready_message | text | InStudio display message before class begins (ex. "Today you'll need a mat and dumbbells") |
| id | integer | Unique primary key of the Occurrence |
| instructor_name | text | Display name of the instructor, if a substitute has been approved, then the name of the substitute instructor |
instructor_id | integer | Numerical ID of the instructor (for InStudio and Livestream classes this can be nil) |
| kind | text | Type of class (ex. InStudio, Livestream, or In-Person) |
| original_instructor_id | integer | Numerical ID of the normally scheduled instructor, if a substitute instructor has been approved for this occurrence |
| original_instructor_name | text | Name of the normally scheduled instructor, if a substitute instructor has been approved for this occurrence |
| program_id | integer | ID of the program |
| published | boolean | Indicates if the occurrence should be displayed |
| repeat_freq | text | Display label for frequency this class is scheduled (ex. "Weekly") |
| schedule_id | integer | ID of the Schedule |
| schedule_name | text | Name of the schedule, allows for multiple calendars to use the same studio (ex. Group Classes, Facility Usage, Daycare, League Play, etc) |
| start_at | datetime | Occurrence start time (when instruction begins). In ISO 8601 format. |
| status | text | scheduled, moved, canceled, or deleted (may be expanded in the future) |
| studio_id | integer | Numerical ID of the Studio |
| studio_name | text | Name of the studio where class will be held (ex. "Studio A") |
| thumbnail_url | text | Program marketing photo that illustrates the activity |
| title | text | Program title (ex. Body Blitz) |
| updated_at | datetime | Last modified date of this occurrence record. In ISO 8601 format. |

### Successful Response

`GET /schedules`

Status: 200

```json
{
    "items": [
        {
            "id": 1869,
            "start_at": "2023-02-18T15:00:00.000Z",
            "end_at": "2023-02-18T15:55:00.000Z",
            "event_id": 132,
            "updated_at": "2023-01-20T17:25:00.583Z",
            "get_ready_message": null,
            "title": "Zumba® Fitness",
            "description": "This Latin-inspired, easy-to-follow, dance-fitness party works all your major body groups in a high-energy cardio blast that leaves you energized, restored and full of life!",
            "thumbnail_url": "https://ymca360.org/api/v3/event/132/image",
            "duration": 3300,
            "program_id": 1,
            "assoc_id": 1,
            "assoc_name": "YMCA360 Studios",
            "branch_id": 1,
            "branch_name": "Downtown",
            "branch_time_zone": "Central Time (US & Canada)",
            "studio_id": 27,
            "studio_name": "Studio A",
            "kind": "In-Person Instructor",
            "repeat_freq": "Every Week",
            "category_id": 2,
            "category_name": "Cardio",
            "instructor_id": 136,
            "instructor_name": "Kristen D",
            "original_instructor_id": null,
            "original_instructor_name": null
        }
    ],
    "summary": {
        "total_items": 100,
        "items_per_page": 10,
        "current_page": 0,
        "total_pages": 9,
        "facets": {
            "studio_ids": [
                {
                    "id": 27,
                    "label": "Studio A"
                }
            ],
            "instructor_ids": [
                {
                    "id": 136,
                    "label": "Kristen D"
                }
            ],
            "assoc_ids": [
                {
                    "id": 1,
                    "label": "YMCA360 Studios"
                }
            ],
            "event_ids": [
                {
                    "id": 132,
                    "label": "Zumba® Fitness"
                }
            ],
            "branch_ids": [
                {
                    "id": 1,
                    "label": "Downtown"
                }
            ],
            "kinds": [
                {
                    "id": "In-Person Instructor",
                    "label": "In-Person Instructor"
                },
                {
                    "id": "InStudio (YMCA360 Virtual Instructor)",
                    "label": "InStudio (YMCA360 Virtual Instructor)"
                }
            ],
            "category_ids": [
                {
                    "id": 2,
                    "label": "Cardio"
                }
            ],
            "program_ids": [
                {
                    "id": 1,
                    "label": "Zumba® Fitness"
                }
            ]
        }
    }
}
```

### Error Response

Status: 401

```json
{
    "error": "Unauthorized"
}
```

## Pagination

* Page numbers are zero-based
* Pagination is based on the `items_per_page`. If `items_per_page=10`, then `page=0` will display the items from 1 to 10, `page=1` will display the items from 11 to 20.
* Pagination is controlled with two params:
    * `page=1` Specify the page to retrieve
    * `size=10` Specify the items per page to retrieve

#### Example Request

`GET /schedules?page=1&size=10`

This request would return 10 items per page and the second page of results with items 11-20.

Pagination information is provide in the summary key of the response.

```js
{
    ...
    "summary": {
        "total_items": 100,
        "items_per_page": 10,
        "current_page": 0,
        "total_pages": 9,
        ...
    }
}
```

## Filters

Results can be filtered using the following parameters:

| Parameter | Type | Default | Notes |
| --- | --- | --- | --- |
| start_at | integer | | An integer value representing the earliest Unix timestamp to include in the results. Items that start at or after this timestamp will be included in the response. |
| end_at | integer | | An integer value representing the latest Unix timestamp to include in the results. Items that end before this timestamp will be included in the response. |
| scheduled_from | integer | current Unix timestamp | An integer value representing the earliest Unix timestamp to include in the results. Items that are scheduled after this timestamp will be included in the response. This includes items currently in progress. |
| updated_at | integer | | An integer value representing the earliest Unix timestamp to include in the results. Items that have been updated at or after this timestamp will be included in the response. |
| assoc_id | integer or Array[integer] | | A single association ID or an array of association IDs to filter by |
| branch_id | integer or Array[integer] | | A single branch ID or an array of branch IDs to filter by |
| category_id | integer or Array[integer] | | A single category ID or an array of category IDs to filter by |
| event_id | integer or Array[integer] | | A single event ID or an array of event IDs to filter by |
| instructor_id | integer or Array[integer] | | A single instructor ID or an array of instructor IDs to filter by |
| kind | string or Array[string] | | A single item type or an array of item types to filter by |
| program_id | integer or Array[integer] | | A single program ID or an array of program IDs to filter by |
| studio_id | integer or Array[integer] | | A single studio ID or an array of studio IDs to filter by |
| search | string | | A full-text search query on title, description, and instructor |


Filters that can be specified as an array can be added in two ways:
* `branch_id=1` will filter results to any items in branch 1
* `branch_id[]=1&branch_id[]=2` will filter results to any items in branch 1 or branch 2

#### Example Request

`GET /schedules?branch_id=1`

This request would return any items in branch 1

## Sorting

You can sort items using the `sort_by` parameter, which currently has two options:

* `sort_by=start_at` to sort items chronologically by their start time, from earliest to latest.
* `sort_by=score` to sort items by their relevance to a search query, with the most relevant items listed first.

The `sort_by=score` option is used in conjunction with the `search` filter. Each item has a `search_score` field that indicates its relevance to the search query.

Results are ordered using `start_at` by default.

## Facets

Facets are provided in the summary key of the response.  Facets are the available options to the [filters](#filters) above.

```js
{
    ...
    "summary": {
        "facets": {
            "studio_ids": [
                {
                    "id": 27,
                    "label": "Studio A"
                }
            ],
            "instructor_ids": [
                {
                    "id": 136,
                    "label": "Kristen D"
                }
            ],
            "assoc_ids": [
                {
                    "id": 1,
                    "label": "YMCA360 Studios"
                }
            ],
            "event_ids": [
                {
                    "id": 132,
                    "label": "Zumba® Fitness"
                }
            ],
            "branch_ids": [
                {
                    "id": 1,
                    "label": "Downtown"
                }
            ],
            "kinds": [
                {
                    "id": "In-Person Instructor",
                    "label": "In-Person Instructor"
                },
                {
                    "id": "InStudio (YMCA360 Virtual Instructor)",
                    "label": "InStudio (YMCA360 Virtual Instructor)"
                }
            ],
            "category_ids": [
                {
                    "id": 2,
                    "label": "Cardio"
                }
            ],
            "program_ids": [
                {
                    "id": 1,
                    "label": "Zumba® Fitness"
                }
            ]
        }
        ...
    }
}
```

