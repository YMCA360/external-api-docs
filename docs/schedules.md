## Group Class Schedules

### Request

`GET /api/external/v1/schedules`

### Successful Response

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
