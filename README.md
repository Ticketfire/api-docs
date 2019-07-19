# TicketFire API

## RESTful Endpoints
| Code | Condition |
| :--- | :-------- |
| DEV | https://int.ticketfire.com |
| STAGE | https://stage.ticketfire.com |
| PROD | https://api2.ticketfire.com |

 DEV & STAGE endpoints are subject to change

## Common Patterns

A HTTP header of `Content-Type: application/json` should be set when making requests.

The API is RESTful and will return the following HTTP status codes in response:

| Code | Condition |
| :--- | :-------- |
| 200 | Success: body contains current model(s) |
| 400 | Bad Request: could not match a valid route |
| 401 | Unauthorized: don't have permission to perform that action |
| 404 | Not Found: either the requested resource does not exist or the user does not have permission to access |
| 500 | Internal Server Error: general response for unexpected errors |

## Requirements
Requires a valid broker account. To sign up, visit:
`{ENDPOINT}/brokers/sign_up`

## Authentication
`POST /users/sign_in`

#### Example Request

    {
    	"user": {
    		"tenant_id": 1,
    		"email": "email@domain.com",
    		"password": "password"
    	}
    }

#### Example Response
##### Successful
`Status: 200 OK`

    {
      "id": 61902,
      "uuid": "54305f18-419d-48b5-bef4-fbda7d08cf94",
      "name": "John Doe",
      "email": "email@domain.com",
      "country_id": 222,
      "phone": "5555555555",
      "is_validated": 0,
      "first_name": "John",
      "last_name": "Doe",
      "tenant_id": 1,
      "authentication_token": "gt7R8Cfnzf6MvxEPUf7C",
      "stripe_customer_id": null
    }
    
##### Error
`Status: 401 Unauthorized`

    {
      "error": "Invalid email or password."
    }

#### Token Usage

When accessing resources that require authentication, two additional HTTP header fields are required.

- `X-User-Email`: value of  `email`
- `X-User-Token`: value of `authentication_token`

## Users

### Update a user
`PUT /users/`

#### Example Request

```
{
	"email": "email@domain.com",
	"phone": "5554443333",
	"first_name": "John",
	"last_name": "Doe",
	"current_password": "trustno1",
	"password" : "password",
	"notify_by_text" : false
}
```
## Ticket Icons (App Background Images)

### List of ticket icons

`GET /ticket_icons`

```
[
  {
    "id": 28,
    "name": "Baseball (College)",
    "url": "https://goo.gl/1rXAeO",
    "updated_at": "2017-02-02T13:58:34.000-05:00"
  },
  {
    "id": 29,
    "name": "Baseball (MLB)",
    "url": "https://goo.gl/1rXAeO",
    "updated_at": "2017-02-02T13:58:34.000-05:00"
  },
  {
    "id": 18,
    "name": "Basketball (College)",
    "url": "https://goo.gl/RwATbV",
    "updated_at": "2017-02-02T13:58:34.000-05:00"
  },
  {
    "id": 19,
    "name": "Basketball (NBA)",
    "url": "https://goo.gl/RwATbV",
    "updated_at": "2017-02-02T13:58:34.000-05:00"
  },
  {
    "id": 27,
    "name": "Concerts",
    "url": "https://goo.gl/v7xykh",
    "updated_at": "2017-02-02T14:00:43.000-05:00"
  },
  {
    "id": 20,
    "name": "Football (College)",
    "url": "https://goo.gl/w1sXHv",
    "updated_at": "2017-02-02T13:58:34.000-05:00"
  },
  {
    "id": 21,
    "name": "Football (NFL)",
    "url": "https://goo.gl/w1sXHv",
    "updated_at": "2017-02-02T13:58:34.000-05:00"
  },
  {
    "id": 33,
    "name": "Formula 1",
    "url": "https://goo.gl/4mRE9P",
    "updated_at": "2017-02-02T13:58:34.000-05:00"
  },
  {
    "id": 22,
    "name": "Hockey",
    "url": "ticket_icon_hockey.png",
    "updated_at": null
  },
  {
    "id": 31,
    "name": "Hockey (College)",
    "url": "https://goo.gl/jm69ja",
    "updated_at": "2017-02-02T13:58:34.000-05:00"
  },
  {
    "id": 30,
    "name": "Hockey (NHL)",
    "url": "https://goo.gl/jm69ja",
    "updated_at": "2017-02-02T13:58:34.000-05:00"
  },
  {
    "id": 32,
    "name": "Nascar",
    "url": "https://goo.gl/SB5hc1",
    "updated_at": "2017-02-02T13:58:34.000-05:00"
  },
  {
    "id": 1,
    "name": "Other",
    "url": "https://goo.gl/jHczWV",
    "updated_at": "2017-02-02T13:58:34.000-05:00"
  },
  {
    "id": 34,
    "name": "Rodeo",
    "url": "https://goo.gl/vZgBem",
    "updated_at": "2017-02-02T13:58:34.000-05:00"
  },
  {
    "id": 23,
    "name": "Soccer (International)",
    "url": "https://goo.gl/tjBt6p",
    "updated_at": "2017-02-02T13:58:34.000-05:00"
  },
  {
    "id": 24,
    "name": "Soccer (MLS)",
    "url": "https://goo.gl/tjBt6p",
    "updated_at": "2017-02-02T13:58:34.000-05:00"
  },
  {
    "id": 26,
    "name": "Theater",
    "url": "https://goo.gl/hqc3v1",
    "updated_at": "2017-02-02T13:58:34.000-05:00"
  },
  {
    "id": 35,
    "name": "Theatre",
    "url": "https://goo.gl/hqc3v1",
    "updated_at": "2017-02-02T13:58:34.000-05:00"
  }
]
```

## Templates

### List of Available PDF Templates

`GET /templates/pdfs/`

#### Example Response

```
{
	"tm": {
		"name": "Template 1",
		"thumbnail": "https://s3.amazonaws.com/ticketfire-storage/website/pdf-examples/template-1-thumb.jpg",
		"example": "https://s3.amazonaws.com/ticketfire-storage/website/pdf-examples/template-1.pdf",
		"shortcode": "tm",
		"custom": false,
		"price": 0.99
	},
	"axs": {
		"name": "Template 2",
		"thumbnail": "https://s3.amazonaws.com/ticketfire-storage/website/pdf-examples/template-2-thumb.jpg",
		"example": "https://s3.amazonaws.com/ticketfire-storage/website/pdf-examples/template-2.pdf",
		"shortcode": "axs",
		"custom": false,
		"price": 0.99
	},
	"ln": {
		"name": "Template 3",
		"thumbnail": "https://s3.amazonaws.com/ticketfire-storage/website/pdf-examples/template-3-thumb.jpg",
		"example": "https://s3.amazonaws.com/ticketfire-storage/website/pdf-examples/template-3.pdf",
		"shortcode": "ln",
		"custom": false,
		"price": 0.99
	},
	"tf": {
		"name": "Template 4",
		"thumbnail": "https://s3.amazonaws.com/ticketfire-storage/website/pdf-examples/template-4-thumb.jpg",
		"example": "https://s3.amazonaws.com/ticketfire-storage/website/pdf-examples/template-4.pdf",
		"shortcode": "tf",
		"custom": false,
		"price": 0.99
	},
	"tc": {
		"name": "Template 5",
		"thumbnail": "https://s3.amazonaws.com/ticketfire-storage/website/pdf-examples/template-5-thumb.jpg",
		"example": "https://s3.amazonaws.com/ticketfire-storage/website/pdf-examples/template-5.pdf",
		"shortcode": "tc",
		"custom": false,
		"price": 0.99
	},
	"stubhub": {
		"name": "StubHub Mobile PDF",
		"thumbnail": "https://s3.amazonaws.com/ticketfire-storage/website/pdf-examples/stubhub-mobile.jpg",
		"example": "https://s3.amazonaws.com/ticketfire-storage/website/pdf-examples/stubhub-mobile.pdf",
		"shortcode": "stubhub",
		"custom": false,
		"price": 0.99
	},
	"aub": {
		"name": "Auburn",
		"thumbnail": "https://s3.amazonaws.com/ticketfire-storage/website/pdf-examples/aub-thumb.jpg",
		"example": "https://s3.amazonaws.com/ticketfire-storage/website/pdf-examples/template-aub.pdf",
		"shortcode": "aub",
		"custom": true,
		"price": 1.99
	},
	"lsu": {
		"name": "LSU",
		"thumbnail": "https://s3.amazonaws.com/ticketfire-storage/website/pdf-examples/lsu-thumb.jpg",
		"example": "https://s3.amazonaws.com/ticketfire-storage/website/pdf-examples/template-lsu.pdf",
		"shortcode": "lsu",
		"custom": true,
		"price": 1.99
	},
	"usc": {
		"name": "USC",
		"thumbnail": "https://s3.amazonaws.com/ticketfire-storage/website/pdf-examples/usc-thumb.jpg",
		"example": "https://s3.amazonaws.com/ticketfire-storage/website/pdf-examples/template-usc.pdf",
		"shortcode": "usc",
		"custom": true,
		"price": 1.99
	},
	"lak": {
		"name": "Los Angeles Kings",
		"thumbnail": "https://s3.amazonaws.com/ticketfire-storage/website/pdf-examples/usc-thumb.jpg",
		"example": "https://s3.amazonaws.com/ticketfire-storage/website/pdf-examples/template-usc.pdf",
		"shortcode": "lak",
		"custom": true,
		"price": 1.99
	}
}

```


## Ticket

### Create a Ticket

`POST /tickets`

### Reasons for failure

 - Not a Valid Ticket
 - Ticket Info Missing From Picture
 - Date Has Expired
 - Image Too Blurry
 - Invalid Barcode
 - Duplicate Ticket

** Notice: `scan_status_id` and `ticket_barcode_data` are NOT present **
`ticket_first_name` and `ticket_last_name` are optional parameters. This is what will be displayed on the PDF as issued to. If these are not set, it will default to the broker's first and last name.

If the `callback_url` parameter is set, the application will `POST` data back to that URL with the data after the ticket has been processed. If the ticket fails, you'll receive a failure message with the reason for failure. If the ticket is successful, you'll receive the a `JSON` object with all of the ticket information.

#### Example Request (with image)

    {
      "ticket_event": "Christmas - A Magical Event",
      "ticket_price": 1000.00,
      "image_file": "http://pathtosome/image.jpg",
      "callback_url": "http://example.com/callback",
      "ticket_venue": "The North Pole",
      "ticket_date": "12/25/2016",
      "ticket_time": "7:00 AM",
      "ticket_time_tbd": null,
      "ticket_section": "TIER4",
      "ticket_row": "L",
      "ticket_seat": "4",
      "ticket_custom_label": "Gate",
      "ticket_custom_value": "North",
      "ticket_first_name": "Santa",
      "ticket_last_name": "Claus",
      "source" : "autoprocessor"
    }


#### Example `POST` to `callback_url` After Ticket Failed Processing

    {
     "failure_reason": "Ticket Info Missing From Picture"
      "id": 111449
      "status": "failed"
    }

#### Example `POST` to `callback_url` After Ticket is Successfully Processed

    {
      "id": 119439,
      "tenant_id": 1,
      "scan_status_id": 2,
      "image_remote": "http://ticketfire-storage.s3.amazonaws.com/tickets/2016/4/9/ticket_349b7f039673457284a59fdd5b55f78b02448298.jpeg",
      "pdf_remote": "{ENDPOINT}/tickets/123.pdf",
      "additional_failure_details": null,
      "barcode_remote": null,
      "ticket_barcode_data": "1234567890",
      "ticket_icon_id": null,
      "ticket_event": "Christmas - A Magical Event",
      "ticket_price": 1000,
      "ticket_venue": "The North Pole",
      "ticket_date": "12/25/2016",
      "ticket_time": "7:00 AM",
      "ticket_time_tbd": null,
      "section_label_id": null,
      "ticket_section": "TIER4",
      "row_label_id": null,
      "ticket_row": "L",
      "seat_label_id": null,
      "ticket_seat": "4",
      "ticket_custom_label": "Gate",
      "ticket_custom_value": "North",
      "created_at": "2016-04-05T14:12:40.000-04:00",
      "unlock_at": null,
      "image_remote_thumbnail": "http://ticketfire-storage.s3.amazonaws.com/tickets/2016/4/9/ticket_4ea990e724c39345966e76eb528e00846b582245.jpeg",
      "apple_wallet_pass_remote": "https://goo.gl/BEjMLT",
      "ticket_first_name": "Santa",
      "ticket_last_name": "Claus",
      image_file_file_name: AdmitOneTicket.jpeg
      "thumbnail": "http://ticketfire-storage.s3.amazonaws.com/tickets/2016/4/9/ticket_4ea990e724c39345966e76eb528e00846b582245.jpeg",
      "ticket_datetime": "2016-12-25T07:00:00.000+00:00",
      "scan_status_name": "Successful",
      "ticket_icon_name": null,
      "section_label_name": null,
      "row_label_name": null,
      "seat_label_name": null,
      "upload_user": {
        "id": 123,
        "name": "John Doe",
        "email": "jdoe@example.com"
      },
      "user": {
        "id": 123,
        "name": "John Doe",
        "email": "jdoe@example.com"
      }
    }

#### Example Request (without image)

    {
      "scan_status_id": 2,
      "ticket_icon_id": 10,
      "ticket_barcode_data": "1234567890",
      "ticket_event": "Christmas - A Magical Event",
      "ticket_price": 1000.00,
      "ticket_venue": "The North Pole",
      "ticket_date": "12/25/2016",
      "ticket_time": "7:00 AM",
      "ticket_time_tbd": null,
      "ticket_section": "TIER4",
      "ticket_row": "L",
      "ticket_seat": "4",
      "ticket_custom_label": "Gate",
      "ticket_custom_value": "North",
      "ticket_first_name": "Santa",
      "ticket_last_name": "Claus",
      "template": "axs"
    }

Setting the `scan_status_id` equal to `2` will bypass the ticket queue.
Please use the `shortcode` from the `/templates/pdfs/` endpoint when setting the `template` param. If no template is set or the template requested does not exist, the `pdf_remote` url will default to Template 1.

#### Example Response
`Status: 200 OK`

    {
      "id": 119439,
      "tenant_id": 1,
      "scan_status_id": 2,
      "image_remote": null,
      "pdf_remote": "{ENDPOINT}/tickets/119439.pdf",
      "additional_failure_details": null,
      "barcode_remote": null,
      "ticket_barcode_data": "1234567890",
      "ticket_icon_id": null,
      "ticket_event": "Christmas - A Magical Event",
      "ticket_price": 1000,
      "ticket_venue": "The North Pole",
      "ticket_date": "12/25/2016",
      "ticket_time": "7:00 AM",
      "ticket_time_tbd": null,
      "section_label_id": null,
      "ticket_section": "TIER4",
      "row_label_id": null,
      "ticket_row": "L",
      "seat_label_id": null,
      "ticket_seat": "4",
      "ticket_custom_label": "Gate",
      "ticket_custom_value": "North",
      "created_at": "2016-04-05T14:12:40.000-04:00",
      "unlock_at": null,
      "image_remote_thumbnail": null,
      "apple_wallet_pass_remote": null,
      "ticket_first_name": "Santa",
      "ticket_last_name": "Claus",
      "template": "axs",
      "thumbnail": null,
      "ticket_datetime": "2016-12-25T07:00:00.000+00:00",
      "scan_status_name": "Successful",
      "ticket_icon_name": null,
      "section_label_name": null,
      "row_label_name": null,
      "seat_label_name": null,
      "upload_user": {
        "id": 61902,
        "name": "John Doe",
        "email": "jdoe@example.com"
      },
      "user": {
        "id": 61902,
        "name": "John Doe",
        "email": "jdoe@example.com"
      }
    }

### Retrieve a Ticket
`GET /tickets/:id/` - To retrieve information about a ticket.
`GET /tickets/:id.pdf` - Sends PDF

#### Example Response
Returns same info as `POST`

### Update a Ticket
`PUT` or `PATCH` -  `/tickets/:id`

#### Example Request

    {
      "ticket_barcode_data": "987654321",
      "ticket_event": "Christmas - A NOT so Magical Event",
      "ticket_first_name": "Jack",
      "ticket_last_name": "Frost"
    }


#### Example Response

    {
      "id": 119439,
      "tenant_id": 1,
      "scan_status_id": 2,
      "image_remote": null,
      "pdf_remote": null,
      "additional_failure_details": null,
      "barcode_remote": null,
      "ticket_barcode_data": "987654321",
      "ticket_icon_id": null,
      "ticket_event": "Christmas - A NOT so Magical Event",
      "ticket_price": 1000,
      "ticket_venue": "The North Pole",
      "ticket_date": "12/25/2016",
      "ticket_time": "7:00 AM",
      "ticket_time_tbd": null,
      "section_label_id": null,
      "ticket_section": "TIER4",
      "row_label_id": null,
      "ticket_row": "L",
      "seat_label_id": null,
      "ticket_seat": "4",
      "ticket_custom_label": "Gate",
      "ticket_custom_value": "North",
      "created_at": "2016-04-05T14:12:40.000-04:00",
      "unlock_at": null,
      "image_remote_thumbnail": null,
      "apple_wallet_pass_remote": null,
      "ticket_first_name": "Santa",
      "ticket_last_name": "Claus",
      "thumbnail": null,
      "ticket_datetime": "2016-12-25T07:00:00.000+00:00",
      "scan_status_name": "Successful",
      "ticket_icon_name": null,
      "section_label_name": null,
      "row_label_name": null,
      "seat_label_name": null,
      "upload_user": {
        "id": 61902,
        "name": "John Doe",
        "email": "jdoe@domain.com"
      },
      "user": {
        "id": 61902,
        "name": "John Doe",
        "email": "jdoe@domain.com"
      }
    }
    
    
### Bulk Create Ticket (in development)
`POST /bulk/tickets`

Must provide a unique `bundle_id`. A `GUID` or `UUID` works great. However, it will be checked for uniqueness. The response body will be blank if successful. Typical bulk requests take < 60 seconds to process and get processed as a background job. This means you'll be responsible for checking the status of the job. See example below on retriving information on a bulk job.

#### Example Request

`Status: 202 Accepted`

    {
      "ticket_event": "Lorem Ipsum",
      "ticket_venue": "Quisque Elit Mauris",
      "ticket_time_tbd": false,
      "scan_status_id": 2,
      "ticket_time": "8:00 AM",
      "ticket_date": "10/12/2016",
      "bundle_id": "c734d7da-28dd-48a0-b231-90bc6bcaa510",
      "seats": [
        {
          "ticket_section": "AMET",
          "ticket_row": 1,
          "ticket_seat": 1,
          "ticket_price": "$422",
          "ticket_barcode": "878097422826",
          "ticket_first_name": "John",
          "ticket_last_name": "Doe"
        },
        {
          "ticket_section": "AMET",
          "ticket_row": 1,
          "ticket_seat": 2,
          "ticket_price": "$236",
          "ticket_barcode": "127893916911",
          "ticket_first_name": "Bobby",
          "ticket_last_name": "Light"
        },
        {
          "ticket_section": "AMET",
          "ticket_row": 1,
          "ticket_seat": 3,
          "ticket_price": "$500",
          "ticket_barcode": "3872820283822",
          "ticket_first_name": "Jane",
          "ticket_last_name": "Doe"
        },
        {
          "ticket_section": "AMET",
          "ticket_row": 1,
          "ticket_seat": 4,
          "ticket_price": "$442",
          "ticket_barcode": "93928487202022",
          "ticket_first_name": "Jim",
          "ticket_last_name": "Nasium"
        },
        {
          "ticket_section": "AMET",
          "ticket_row": 1,
          "ticket_seat": 5,
          "ticket_price": "$300",
          "ticket_barcode": "028482847228482",
          "ticket_first_name": "Hank",
          "ticket_last_name": "Hill"
        }
      ]
    }
    
### Retrieve Bulk Information (in development)
`GET /bulk/tickets/:bundle_id`

#### Example Response

Note the `status` key will contain information as to wheter the job has finished or if it's still being processed.

`Status: 200 OK`

**Job Processing**

    {
      "id": 6,
      "bundle_id": "5e6be1e8-7a85-4ed9-ac09-58d13182d766",
      "status": "processing",
      "created_at": "2016-04-19T15:42:51.000-04:00"
    }

**Job Complete**

    {
      "id": 13,
      "bundle_id": "c734d7da-28dd-48a0-b231-90bc6bcaa510",
      "status": "complete",
      "created_at": "2016-04-20T11:17:22.000-04:00",
      "tickets": [
        {
          "id": 1865,
          "tenant_id": 1,
          "scan_status_id": 2,
          "image_remote": null,
          "pdf_remote": "http://example.com/tickets/1865.pdf",
          "additional_failure_details": null,
          "barcode_remote": null,
          "ticket_barcode_data": "878097422826",
          "ticket_icon_id": null,
          "ticket_event": "Lorem Ipsum",
          "ticket_price": 0,
          "ticket_venue": "Quisque Elit Mauris",
          "ticket_date": "10/12/2016",
          "ticket_time": "8:00 AM",
          "ticket_time_tbd": false,
          "section_label_id": null,
          "ticket_section": "AMET",
          "row_label_id": null,
          "ticket_row": "1",
          "seat_label_id": null,
          "ticket_seat": "1",
          "ticket_custom_label": null,
          "ticket_custom_value": null,
          "created_at": "2016-04-20T11:17:22.000-04:00",
          "unlock_at": null,
          "image_remote_thumbnail": null,
          "apple_wallet_pass_remote": null,
          "ticket_first_name": "John",
          "ticket_last_name": "Doe",
          "thumbnail": null,
          "ticket_datetime": "2016-10-12T08:00:00.000+00:00",
          "scan_status_name": "Success",
          "ticket_icon_name": null,
          "section_label_name": null,
          "row_label_name": null,
          "seat_label_name": null,
          "upload_user": {
            "id": 1,
            "name": "John Doe",
            "email": "jdoe@example.com"
          },
          "user": {
            "id": 1,
            "name": "John Doe",
            "email": "jdoe@example.com"
          }
        },
        {
          "id": 1866,
          "tenant_id": 1,
          "scan_status_id": 2,
          "image_remote": null,
          "pdf_remote": "http://example.com/tickets/1866.pdf",
          "additional_failure_details": null,
          "barcode_remote": null,
          "ticket_barcode_data": "127893916911",
          "ticket_icon_id": null,
          "ticket_event": "Lorem Ipsum",
          "ticket_price": 0,
          "ticket_venue": "Quisque Elit Mauris",
          "ticket_date": "10/12/2016",
          "ticket_time": "8:00 AM",
          "ticket_time_tbd": false,
          "section_label_id": null,
          "ticket_section": "AMET",
          "row_label_id": null,
          "ticket_row": "1",
          "seat_label_id": null,
          "ticket_seat": "2",
          "ticket_custom_label": null,
          "ticket_custom_value": null,
          "created_at": "2016-04-20T11:17:22.000-04:00",
          "unlock_at": null,
          "image_remote_thumbnail": null,
          "apple_wallet_pass_remote": null,
          "ticket_first_name": "Bobby",
          "ticket_last_name": "Light",
          "thumbnail": null,
          "ticket_datetime": "2016-10-12T08:00:00.000+00:00",
          "scan_status_name": "Success",
          "ticket_icon_name": null,
          "section_label_name": null,
          "row_label_name": null,
          "seat_label_name": null,
          "upload_user": {
            "id": 1,
            "name": "John Doe",
            "email": "jdoe@example.com"
          },
          "user": {
            "id": 1,
            "name": "John Doe",
            "email": "jdoe@example.com"
          }
        },
        {
          "id": 1867,
          "tenant_id": 1,
          "scan_status_id": 2,
          "image_remote": null,
          "pdf_remote": "http://example.com/tickets/1867.pdf",
          "additional_failure_details": null,
          "barcode_remote": null,
          "ticket_barcode_data": "3872820283822",
          "ticket_icon_id": null,
          "ticket_event": "Lorem Ipsum",
          "ticket_price": 0,
          "ticket_venue": "Quisque Elit Mauris",
          "ticket_date": "10/12/2016",
          "ticket_time": "8:00 AM",
          "ticket_time_tbd": false,
          "section_label_id": null,
          "ticket_section": "AMET",
          "row_label_id": null,
          "ticket_row": "1",
          "seat_label_id": null,
          "ticket_seat": "3",
          "ticket_custom_label": null,
          "ticket_custom_value": null,
          "created_at": "2016-04-20T11:17:22.000-04:00",
          "unlock_at": null,
          "image_remote_thumbnail": null,
          "apple_wallet_pass_remote": null,
          "ticket_first_name": "Jane",
          "ticket_last_name": "Doe",
          "thumbnail": null,
          "ticket_datetime": "2016-10-12T08:00:00.000+00:00",
          "scan_status_name": "Success",
          "ticket_icon_name": null,
          "section_label_name": null,
          "row_label_name": null,
          "seat_label_name": null,
          "upload_user": {
            "id": 1,
            "name": "John Doe",
            "email": "jdoe@example.com"
          },
          "user": {
            "id": 1,
            "name": "John Doe",
            "email": "jdoe@example.com"
          }
        },
        {
          "id": 1868,
          "tenant_id": 1,
          "scan_status_id": 2,
          "image_remote": null,
          "pdf_remote": "http://example.com/tickets/1868.pdf",
          "additional_failure_details": null,
          "barcode_remote": null,
          "ticket_barcode_data": "93928487202022",
          "ticket_icon_id": null,
          "ticket_event": "Lorem Ipsum",
          "ticket_price": 0,
          "ticket_venue": "Quisque Elit Mauris",
          "ticket_date": "10/12/2016",
          "ticket_time": "8:00 AM",
          "ticket_time_tbd": false,
          "section_label_id": null,
          "ticket_section": "AMET",
          "row_label_id": null,
          "ticket_row": "1",
          "seat_label_id": null,
          "ticket_seat": "4",
          "ticket_custom_label": null,
          "ticket_custom_value": null,
          "created_at": "2016-04-20T11:17:22.000-04:00",
          "unlock_at": null,
          "image_remote_thumbnail": null,
          "apple_wallet_pass_remote": null,
          "ticket_first_name": "Jim",
          "ticket_last_name": "Nasium",
          "thumbnail": null,
          "ticket_datetime": "2016-10-12T08:00:00.000+00:00",
          "scan_status_name": "Success",
          "ticket_icon_name": null,
          "section_label_name": null,
          "row_label_name": null,
          "seat_label_name": null,
          "upload_user": {
            "id": 1,
            "name": "John Doe",
            "email": "jdoe@example.com"
          },
          "user": {
            "id": 1,
            "name": "John Doe",
            "email": "jdoe@example.com"
          }
        },
        {
          "id": 1869,
          "tenant_id": 1,
          "scan_status_id": 2,
          "image_remote": null,
          "pdf_remote": "http://example.com/tickets/1869.pdf",
          "additional_failure_details": null,
          "barcode_remote": null,
          "ticket_barcode_data": "028482847228482",
          "ticket_icon_id": null,
          "ticket_event": "Lorem Ipsum",
          "ticket_price": 0,
          "ticket_venue": "Quisque Elit Mauris",
          "ticket_date": "10/12/2016",
          "ticket_time": "8:00 AM",
          "ticket_time_tbd": false,
          "section_label_id": null,
          "ticket_section": "AMET",
          "row_label_id": null,
          "ticket_row": "1",
          "seat_label_id": null,
          "ticket_seat": "5",
          "ticket_custom_label": null,
          "ticket_custom_value": null,
          "created_at": "2016-04-20T11:17:22.000-04:00",
          "unlock_at": null,
          "image_remote_thumbnail": null,
          "apple_wallet_pass_remote": null,
          "ticket_first_name": "Hank",
          "ticket_last_name": "Hill",
          "thumbnail": null,
          "ticket_datetime": "2016-10-12T08:00:00.000+00:00",
          "scan_status_name": "Success",
          "ticket_icon_name": null,
          "section_label_name": null,
          "row_label_name": null,
          "seat_label_name": null,
          "upload_user": {
            "id": 1,
            "name": "John Doe",
            "email": "jdoe@example.com"
          },
          "user": {
            "id": 1,
            "name": "John Doe",
            "email": "jdoe@example.com"
          }
        }
      ]
    }
